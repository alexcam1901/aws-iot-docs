# Configuring a remote device and using IoT agent<a name="configure-remote-device"></a>

The IoT agent is used to receive the MQTT message that includes the client access token and start a local proxy on the remote device\. You must install and run the IoT agent on the remote device if you want secure tunneling to deliver the client access token using MQTT\. The IoT agent must subscribe to the following reserved IoT MQTT topic:

**Note**  
If you want to deliver the destination client access token to the remote device through methods other than subscribing to the reserved MQTT topic, you might need a destination client access token \(CAT\) listener and a local proxy\. The CAT listener must work with your chosen client access token delivery mechanism and be able to start a local proxy in destination mode\.

## IoT agent snippet<a name="agent-snippet"></a>

The IoT agent must subscribe to the following reserved IoT MQTT topic so that it can receive the MQTT message and start the local proxy:

`$aws/things/thing-name/tunnels/notify`

Where `thing-name` is the name of AWS IoT thing associated with the remote device\.

The following is an example MQTT message payload:

```
{
    "clientAccessToken": "destination-client-access-token",
    "clientMode": "destination",
    "region": "aws-region",
    "services": ["destination-service"]
}
```

After it receives an MQTT message, the IoT agent must start a local proxy on the remote device with the appropriate parameters\.

The following Java code demonstrates how to use the [AWS IoT Device SDK](https://github.com/aws/aws-iot-device-sdk-java) and [ProcessBuilder](https://docs.oracle.com/javase/8/docs/api/java/lang/ProcessBuilder.html) from the Java library to build a simple IoT agent to work with secure tunneling\.

```
// Find the IoT device endpoint for your AWS account
final String endpoint = iotClient.describeEndpoint(new DescribeEndpointRequest().withEndpointType("iot:Data-ATS")).getEndpointAddress();

// Instantiate the IoT Agent with your AWS credentials
final String thingName = "RemoteDeviceA";
final String tunnelNotificationTopic = String.format("$aws/things/%s/tunnels/notify", thingName);
final AWSIotMqttClient mqttClient = new AWSIotMqttClient(endpoint, thingName,
                 "your_aws_access_key", "your_aws_secret_key");

try {
    mqttClient.connect();
    final TunnelNotificationListener listener = new TunnelNotificationListener(tunnelNotificationTopic);
    mqttClient.subscribe(listener, true);
}
finally {
    mqttClient.disconnect();
}

private static class TunnelNotificationListener extends AWSIotTopic {
    public TunnelNotificationListener(String topic) {
        super(topic);
    }

    @Override
    public void onMessage(AWSIotMessage message) {
        try {
            // Deserialize the MQTT message
            final JSONObject json = new JSONObject(message.getStringPayload());
 
            final String accessToken = json.getString("clientAccessToken");
            final String region = json.getString("region");
            
            final String clientMode = json.getString("clientMode");
            if (!clientMode.equals("destination")) {
                throw new RuntimeException("Client mode " + clientMode + " in the MQTT message is not expected");
            }

            final JSONArray servicesArray = json.getJSONArray("services");
            if (servicesArray.length() > 1) {
                throw new RuntimeException("Services in the MQTT message has more than 1 service");
            }
            final String service = servicesArray.get(0).toString();
            if (!service.equals("SSH")) {
                throw new RuntimeException("Service " + service + " is not supported");
            }

            // Start the destination local proxy in a separate process to connect to the SSH Daemon listening port 22
            final ProcessBuilder pb = new ProcessBuilder("localproxy",
                        "-t", accessToken,
                        "-r", region,
                        "-d", "localhost:22");
            pb.start();
        }
        catch (Exception e) {
            log.error("Failed to start the local proxy", e);
        }
    }
}
```