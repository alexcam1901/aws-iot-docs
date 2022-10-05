# Using AWS IoT Device Defender with other AWS services<a name="dd-integration"></a>

## Using AWS IoT Device Defender with devices running AWS IoT Greengrass<a name="dd-gg-integration"></a>

AWS IoT Greengrass provides pre\-built integration with AWS IoT Device Defender to monitor device behaviors on an ongoing basis\.
+ [Integrate Device Defender with AWS IoT Greengrass V1](https://docs.aws.amazon.com/greengrass/v1/developerguide/device-defender-connector.html)
+ [Integrate Device Defender with AWS IoT Greengrass V2](https://docs.aws.amazon.com/greengrass/v2/developerguide/device-defender-component.html)

## Using AWS IoT Device Defender with FreeRTOS and embedded devices<a name="dd-integration-FreeRTOS"></a>

To use AWS IoT Device Defender on a FreeRTOS device, your device must have the [FreeRTOS Embedded C SDK](https://github.com/aws/amazon-freertos) or the [AWS IoT Device Defender library](https://docs.aws.amazon.com/embedded-csdk/latest/lib-ref/libraries/aws/device-defender-for-aws-iot-embedded-sdk/docs/doxygen/output/html/index.html) installed\. The FreeRTOS Embedded C SDK includes the AWS IoT Device Defender library\. For information about how to integrate AWS IoT Device Defender with your FreeRTOS devices, see the following demos:


+ [AWS IoT Device Defender for FreeRTOS standard metrics and custom metrics demos](https://freertos.org/iot-device-defender-demo.html)
+ [Using MQTT agent to submit metrics to AWS IoT Device Defender](https://freertos.org/iot-device-defender/demo-with-mqtt-agent.html)
+ [Using the MQTT core library to submit metrics to AWS IoT Device Defender](https://docs.aws.amazon.com/freertos/latest/userguide/dd-demo.html)

To use AWS IoT Device Defender on an embedded device without FreeRTOS, your device must have the [AWS IoT Embedded C SDK](https://docs.aws.amazon.com/iot/latest/developerguide/iot-embedded-c-sdk.html) or [AWS IoT Device Defender library](https://docs.aws.amazon.com/embedded-csdk/latest/lib-ref/libraries/aws/device-defender-for-aws-iot-embedded-sdk/docs/doxygen/output/html/index.html)\. The AWS IoT Embedded C SDK includes the AWS IoT Device Defender library\. For information about how to integrate AWS IoT Device Defender with your embedded devices, see the following demos, [AWS IoT Device Defender for AWS IoT Embedded SDK standard and custom metrics demos](https://github.com/aws/aws-iot-device-sdk-embedded-C/blob/main/docs/doxygen/demos/defender_demo.dox)\.

## Using AWS IoT Device Defender with AWS IoT Device Management<a name="dd-integration-device-management"></a>

You can use AWS IoT Device Management fleet indexing to index, search, and aggregate your AWS IoT Device Defender detect violations\. After your Device Defender violations data is indexed in fleet indexing, you can access and query Device Defender violations data from Fleet Hub applications, create fleet alarms based on violations data to monitor anomalies across your fleet of devices, and view fleet alarms in Fleet Hub dashboards\. 

**Note**  
The fleet indexing feature to support indexing AWS IoT Device Defender violations data is in preview release for AWS IoT Device Management and is subject to change\.
+ [Managing fleet indexing](https://docs.aws.amazon.com/iot/latest/developerguide/managing-fleet-index.html)
+ [Query syntax](https://docs.aws.amazon.com/iot/latest/developerguide/query-syntax.html)
+ [Managing fleet indexing for Fleet Hub applications](https://docs.aws.amazon.com/iot/latest/fleethubuserguide/aws-iot-monitor-admin-fleet-indexing.html)
+ [Getting started](https://docs.aws.amazon.com/iot/latest/fleethubuserguide/aws-iot-monitor-user-getting-started.html)