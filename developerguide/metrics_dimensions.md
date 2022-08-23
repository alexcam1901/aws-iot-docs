# AWS IoT metrics and dimensions<a name="metrics_dimensions"></a>

When you interact with AWS IoT, the service sends the following metrics and dimensions to CloudWatch every minute\. You can use the following procedures to view the metrics for AWS IoT\.

**To view metrics \(CloudWatch console\)**

Metrics are grouped first by the service namespace, and then by the various dimension combinations within each namespace\.

1. Open the [CloudWatch console](https://console.aws.amazon.com/cloudwatch)\.

1. In the navigation pane, choose **Metrics** and then choose **All metrics**\.

1. In the **Browse** tab, search for AWS IoT to view the list of metrics\.

**To view metrics \(CLI\)**
+ At a command prompt, use the following command:

  ```
  1. aws cloudwatch list-metrics --namespace "AWS/IoT"
  ```

**Topics**
+ [AWS IoT metrics](#iot-metrics)
+ [AWS IoT Core credential provider metrics](#credential-provider-metrics)
+ [Rule metrics](#rulemetrics)
+ [Rule action metrics](#rule-action-metrics)
+ [HTTP action specific metrics](#http-action-metrics)
+ [Message broker metrics](#message-broker-metrics)
+ [Device shadow metrics](#shadow-metrics)
+ [Jobs metrics](#jobs-metrics)
+ [Device Defender audit metrics](#device-defender-audit-metrics)
+ [Device Defender detect metrics](#device-defender-detect-metrics)
+ [Device provisioning metrics](#provisioning-metrics)
+ [Fleet indexing metrics](#fleet-indexing-metrics)
+ [Dimensions for metrics](#aws-iot-metricdimensions)

## AWS IoT metrics<a name="iot-metrics"></a>


| Metric | Description | 
| --- | --- | 
|  `AddThingToDynamicThingGroupsFailed`  |  The number of failure events associated with adding a thing to a dynamic thing group\. The `DynamicThingGroupName` dimension contains the name of the dynamic groups that failed to add things\.  | 
|  `NumLogBatchesFailedToPublishThrottled`  |  The singular batch of log events that has failed to publish due to throttling errors\.  | 
|  `NumLogEventsFailedToPublishThrottled`  |  The number of log events within the batch that have failed to publish due to throttling errors\.  | 

## AWS IoT Core credential provider metrics<a name="credential-provider-metrics"></a>


| Metric | Description | 
| --- | --- | 
|  `CredentialExchangeSuccess`  |  The number of successful `AssumeRoleWithCertificate` requests to AWS IoT Core credentials provider\.  | 

## Rule metrics<a name="rulemetrics"></a>


| Metric | Description | 
| --- | --- | 
|  `ParseError`  |  The number of JSON parse errors that occurred in messages published on a topic on which a rule is listening\. The `RuleName` dimension contains the name of the rule\.  | 
|  `RuleMessageThrottled`  |  The number of messages throttled by the rules engine because of malicious behavior or because the number of messages exceeds the rules engine's throttle limit\. The `RuleName` dimension contains the name of the rule to be triggered\.  | 
|  `RuleNotFound`  |  The rule to be triggered could not be found\. The `RuleName` dimension contains the name of the rule\.  | 
|  `RulesExecuted`  |  The number of AWS IoT rules executed\.  | 
|  `TopicMatch`  |  The number of incoming messages published on a topic on which a rule is listening\. The `RuleName` dimension contains the name of the rule\.  | 

## Rule action metrics<a name="rule-action-metrics"></a>


| Metric | Description | 
| --- | --- | 
|  `Failure`  |  The number of failed rule action invocations\. The `RuleName` dimension contains the name of the rule that specifies the action\. The `ActionType` dimension contains the type of action that was invoked\.  | 
|  `Success`  |  The number of successful rule action invocations\. The `RuleName` dimension contains the name of the rule that specifies the action\. The `ActionType` dimension contains the type of action that was invoked\.  | 
| ErrorActionFailure | The number of failed error actions\. The RuleName dimension contains the name of the rule that specifies the action\. The ActionType dimension contains the type of action that was invoked\. | 
| ErrorActionSuccess | The number of successful error actions\. The RuleName dimension contains the name of the rule that specifies the action\. The ActionType dimension contains the type of action that was invoked\. | 

## HTTP action specific metrics<a name="http-action-metrics"></a>


| Metric | Description | 
| --- | --- | 
|  `HttpCode_Other`  |  Generated if the status code of the response from the downstream web service/application is not 2xx, 4xx or 5xx\.  | 
|  `HttpCode_4XX`  |  Generated if the status code of the response from the downstream web service/application is between 400 and 499\.  | 
|  `HttpCode_5XX`  |  Generated if the status code of the response from the downstream web service/application is between 500 and 599\.  | 
|  `HttpInvalidUrl`  |  Generated if an endpoint URL, after substitution templates are replaced, does not start with `https://`\.  | 
|  `HttpRequestTimeout`  |  Generated if the downstream web service/application does not return response within request timeout limit\. For more information, see [Service Quotas](https://docs.aws.amazon.com/general/latest/gr/iot-core.html#limits_iot)\.  | 
|  `HttpUnknownHost`  |  Generated if the URL is valid, but the service does not exist or is unreachable\.  | 

## Message broker metrics<a name="message-broker-metrics"></a>

**Note**  
The message broker metrics are displayed in the CloudWatch console under **Protocol Metrics**\.


| Metric | Description | 
| --- | --- | 
|  `Connect.AuthError`  |  The number of connection requests that could not be authorized by the message broker\. The `Protocol` dimension contains the protocol used to send the `CONNECT` message\.  | 
|  `Connect.ClientError`  |  The number of connection requests rejected because the MQTT message did not meet the requirements defined in [AWS IoT quotas](limits-iot.md)\. The `Protocol` dimension contains the protocol used to send the `CONNECT` message\.  | 
|  `Connect.ClientIDThrottle`  |  The number of connection requests throttled because the client exceeded the allowed connect request rate for a specific client ID\. The `Protocol` dimension contains the protocol used to send the `CONNECT` message\.  | 
|  `Connect.ServerError`  |  The number of connection requests that failed because an internal error occurred\. The `Protocol` dimension contains the protocol used to send the `CONNECT` message\.  | 
|  `Connect.Success`  |  The number of successful connections to the message broker\. The `Protocol` dimension contains the protocol used to send the `CONNECT` message\.  | 
|  `Connect.Throttle`  |  The number of connection requests that were throttled because the account exceeded the allowed connect request rate\. The `Protocol` dimension contains the protocol used to send the `CONNECT` message\.  | 
|  `Ping.Success`  |  The number of ping messages received by the message broker\. The `Protocol` dimension contains the protocol used to send the ping message\.  | 
|  `PublishIn.AuthError`  |  The number of publish requests the message broker was unable to authorize\. The `Protocol` dimension contains the protocol used to publish the message\.  | 
|  `PublishIn.ClientError`  |  The number of publish requests rejected by the message broker because the message did not meet the requirements defined in [AWS IoT quotas](limits-iot.md)\. The `Protocol` dimension contains the protocol used to publish the message\.  | 
|  `PublishIn.ServerError`  |  The number of publish requests the message broker failed to process because an internal error occurred\. The `Protocol` dimension contains the protocol used to send the `PUBLISH` message\.  | 
|  `PublishIn.Success`  |  The number of publish requests successfully processed by the message broker\. The `Protocol` dimension contains the protocol used to send the `PUBLISH` message\.  | 
|  `PublishIn.Throttle`  |  The number of publish request that were throttled because the client exceeded the allowed inbound message rate\. The `Protocol` dimension contains the protocol used to send the `PUBLISH` message\.  | 
|  `PublishOut.AuthError`  |  The number of publish requests made by the message broker that could not be authorized by AWS IoT\. The `Protocol` dimension contains the protocol used to send the `PUBLISH` message\.  | 
|  `PublishOut.ClientError`  |  The number of publish requests made by the message broker that were rejected because the message did not meet the requirements defined in [AWS IoT quotas](limits-iot.md)\. The `Protocol` dimension contains the protocol used to send the `PUBLISH` message\.  | 
|  `PublishOut.Success`  |  The number of publish requests successfully made by the message broker\. The `Protocol` dimension contains the protocol used to send the `PUBLISH` message\.  | 
| PublishOut\.Throttle |  The number of publish requests that were throttled because the client exceeded the allowed outbound message rate\. The `Protocol` dimension contains the protocol used to send the `PUBLISH` message\.  | 
|  `PublishRetained.AuthError`  |  The number of publish requests with the `RETAIN` flag set that the message broker was unable to authorize\. The `Protocol` dimension contains the protocol used to send the `PUBLISH` message\.  | 
| PublishRetained\.ServerError |  The number of retained publish requests the message broker failed to process because an internal error occurred\. The `Protocol` dimension contains the protocol used to send the `PUBLISH` message\.  | 
|  `PublishRetained.Success`  |  The number of publish requests with the `RETAIN` flag set that were successfully processed by the message broker\. The `Protocol` dimension contains the protocol used to send the `PUBLISH` message\.  | 
|  `PublishRetained.Throttle`  |  The number of publish requests with the `RETAIN` flag set that were throttled because the client exceeded the allowed inbound message rate\. The `Protocol` dimension contains the protocol used to send the `PUBLISH` message\.  | 
|  `Subscribe.AuthError`  |  The number of subscription requests made by a client that could not be authorized\. The `Protocol` dimension contains the protocol used to send the `SUBSCRIBE` message\.  | 
|  `Subscribe.ClientError`  |  The number of subscribe requests that were rejected because the `SUBSCRIBE` message did not meet the requirements defined in [AWS IoT quotas](limits-iot.md)\. The `Protocol` dimension contains the protocol used to send the `SUBSCRIBE` message\.  | 
|  `Subscribe.ServerError`  |  The number of subscribe requests that were rejected because an internal error occurred\. The `Protocol` dimension contains the protocol used to send the `SUBSCRIBE` message\.  | 
|  `Subscribe.Success`  |  The number of subscribe requests that were successfully processed by the message broker\. The `Protocol` dimension contains the protocol used to send the `SUBSCRIBE` message\.  | 
|  `Subscribe.Throttle`  |  The number of subscribe requests that were throttled because the client exceeded the allowed subscribe request rate\. The `Protocol` dimension contains the protocol used to send the `SUBSCRIBE` message\.  | 
|  `Unsubscribe.ClientError`  |  The number of unsubscribe requests that were rejected because the `UNSUBSCRIBE` message did not meet the requirements defined in [AWS IoT quotas](limits-iot.md)\. The `Protocol` dimension contains the protocol used to send the `UNSUBSCRIBE` message\.  | 
|  `Unsubscribe.ServerError`  |  The number of unsubscribe requests that were rejected because an internal error occurred\. The `Protocol` dimension contains the protocol used to send the `UNSUBSCRIBE` message\.  | 
|  `Unsubscribe.Success`  |  The number of unsubscribe requests that were successfully processed by the message broker\. The `Protocol` dimension contains the protocol used to send the `UNSUBSCRIBE` message\.  | 
|  `Unsubscribe.Throttle`  |  The number of unsubscribe requests that were rejected because the client exceeded the allowed unsubscribe request rate\. The `Protocol` dimension contains the protocol used to send the `UNSUBSCRIBE` message\.   | 

## Device shadow metrics<a name="shadow-metrics"></a>

**Note**  
The device shadow metrics are displayed in the CloudWatch console under **Protocol Metrics**\.


| Metric | Description | 
| --- | --- | 
|  `DeleteThingShadow.Accepted`  |  The number of `DeleteThingShadow` requests processed successfully\. The `Protocol` dimension contains the protocol used to make the request\.  | 
|  `GetThingShadow.Accepted`  |  The number of `GetThingShadow` requests processed successfully\. The `Protocol` dimension contains the protocol used to make the request\.  | 
|  `ListThingShadow.Accepted`  |  The number of `ListThingShadow` requests processed successfully\. The `Protocol` dimension contains the protocol used to make the request\.  | 
|  `UpdateThingShadow.Accepted`  |  The number of `UpdateThingShadow` requests processed successfully\. The `Protocol` dimension contains the protocol used to make the request\.  | 

## Jobs metrics<a name="jobs-metrics"></a>


| Metric | Description | 
| --- | --- | 
|  `CanceledJobExecutionCount`  |  The number of job executions whose status has changed to `CANCELED` within a time period that is determined by CloudWatch\. \(For more information about CloudWatch metrics, see [Amazon CloudWatch Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Metric)\.\) The `JobId` dimension contains the ID of the job\.  | 
|  `CanceledJobExecutionTotalCount`  |  The total number of job executions whose status is `CANCELED` for the given job\. The `JobId` dimension contains the ID of the job\.  | 
|  `ClientErrorCount`  |  The number of client errors generated while executing the job\. The `JobId` dimension contains the ID of the job\.  | 
|  `FailedJobExecutionCount`  |  The number of job executions whose status has changed to `FAILED` within a time period that is determined by CloudWatch\. \(For more information about CloudWatch metrics, see [Amazon CloudWatch Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Metric)\.\) The `JobId` dimension contains the ID of the job\.  | 
|  `FailedJobExecutionTotalCount`  |  The total number of job executions whose status is `FAILED` for the given job\. The `JobId` dimension contains the ID of the job\.  | 
|  `InProgressJobExecutionCount`  |  The number of job executions whose status has changed to `IN_PROGRESS` within a time period that is determined by CloudWatch\. \(For more information about CloudWatch metrics, see [Amazon CloudWatch Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Metric)\.\) The `JobId` dimension contains the ID of the job\.  | 
|  `InProgressJobExecutionTotalCount`  |  The total number of job executions whose status is `IN_PROGRESS` for the given job\. The `JobId` dimension contains the ID of the job\.  | 
|  `RejectedJobExecutionTotalCount`  |  The total number of job executions whose status is `REJECTED` for the given job\. The `JobId` dimension contains the ID of the job\.  | 
|  `RemovedJobExecutionTotalCount`  |  The total number of job executions whose status is `REMOVED` for the given job\. The `JobId` dimension contains the ID of the job\.  | 
|  `QueuedJobExecutionCount`  |  The number of job executions whose status has changed to `QUEUED` within a time period that is determined by CloudWatch\. \(For more information about CloudWatch metrics, see [Amazon CloudWatch Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Metric)\.\) The `JobId` dimension contains the ID of the job\.  | 
|  `QueuedJobExecutionTotalCount`  |  The total number of job executions whose status is `QUEUED` for the given job\. The `JobId` dimension contains the ID of the job\.  | 
|  `RejectedJobExecutionCount`  |  The number of job executions whose status has changed to `REJECTED` within a time period that is determined by CloudWatch\. \(For more information about CloudWatch metrics, see [Amazon CloudWatch Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Metric)\.\) The `JobId` dimension contains the ID of the job\.  | 
|  `RemovedJobExecutionCount`  |  The number of job executions whose status has changed to `REMOVED` within a time period that is determined by CloudWatch\. \(For more information about CloudWatch metrics, see [Amazon CloudWatch Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Metric)\.\) The `JobId` dimension contains the ID of the job\.  | 
|  `ServerErrorCount`  |  The number of server errors generated while executing the job\. The `JobId` dimension contains the ID of the job\.  | 
|  `SuccededJobExecutionCount`  |  The number of job executions whose status has changed to `SUCCESS` within a time period that is determined by CloudWatch\. \(For more information about CloudWatch metrics, see [Amazon CloudWatch Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Metric)\.\) The `JobId` dimension contains the ID of the job\.  | 
|  `SuccededJobExecutionTotalCount`  |  The total number of job executions whose status is `SUCCESS` for the given job\. The `JobId` dimension contains the ID of the job\.  | 

## Device Defender audit metrics<a name="device-defender-audit-metrics"></a>


| Metric | Description | 
| --- | --- | 
|  `NonCompliantResources`  |  The number of resources that were found to be noncompliant with a check\. The system reports the number of resources that were out of compliance for each check of each audit performed\.   | 
|  `ResourcesEvaluated`  |  The number of resources that were evaluated for compliance\. The system reports the number of resources that were evaluated for each check of each audit performed\.   | 

## Device Defender detect metrics<a name="device-defender-detect-metrics"></a>


| Metric | Description | 
| --- | --- | 
|  `Violations`   |  The number of new violations of security profile behaviors that have been found since the last time an evaluation was performed\. The system reports the number of new violations for the account, for a specific security profile, and for a specific behavior of a specific security profile\.   | 
|  `ViolationsCleared`   |  The number of violations of security profile behaviors that have been resolved since the last time an evaluation was performed\. The system reports the number of resolved violations for the account, for a specific security profile, and for a specific behavior of a specific security profile\.   | 
|  `ViolationsInvalidated`   |  The number of violations of security profile behaviors for which information is no longer available since the last time an evaluation was performed \(because the reporting device stopped reporting, or is no longer being monitored for some reason\)\. The system reports the number of invalidated violations for the entire account, for a specific security profile, and for a specific behavior of a specific security profile\.   | 

## Device provisioning metrics<a name="provisioning-metrics"></a>


**AWS IoT Fleet provisioning metrics**  

| Metric | Description | 
| --- | --- | 
|  `ApproximateNumberOfThingsRegistered`  |  The count of things that have been registered by Fleet Provisioning\. While the count is generally accurate, the distributed architecture of AWS IoT Core makes it difficult to maintain a precise count of registered things\.  The statistic to use for this metric is: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot/latest/developerguide/metrics_dimensions.html)  Dimensions: [ClaimCertificateId](#aws-iot-metricdimensions)  | 
|  `CreateKeysAndCertificateFailed`  |  The number of failures that occurred by calls to the `CreateKeysAndCertificate` MQTT API\. The metric is emitted in both Success \(value = 0\) and Failure \(value = 1\) cases\. This metric can be used to track the number of certificates created and registered during the CloudWatch\-supported aggregation windows, such as 5 min\. or 1 hour\. The statistics available for this metric are: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot/latest/developerguide/metrics_dimensions.html)  | 
|  `CreateCertificateFromCsrFailed`  |  The number of failures that occurred by calls to the `CreateCertificateFromCsr` MQTT API\. The metric is emitted in both Success \(value = 0\) and Failure \(value = 1\) cases\. This metric can be used to track the number of things registered during the CloudWatch\-supported aggregation windows, such as 5 min\. or 1 hour\.  The statistics available for this metric are: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot/latest/developerguide/metrics_dimensions.html)  | 
|  `RegisterThingFailed`  |  The number of failures that occurred by calls to the `RegisterThing` MQTT API\. The metric is emitted in both Success \(value = 0\) and Failure \(value = 1\) cases\. This metric can be used to track the number of things registered during the CloudWatch\-supported aggregation windows, such as 5 min\. or 1 hour\. For the total number of things registered , see the `ApproximateNumberOfThingsRegistered` metric\. The statistics available for this metric are: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot/latest/developerguide/metrics_dimensions.html) Dimensions: [TemplateName](#aws-iot-metricdimensions)  | 


**Just\-in\-time provisioning metrics**  

| Metric | Description | 
| --- | --- | 
|  `ProvisionThing.ClientError`  |  The number of times a device failed to provision due to a client error\. For example, the policy specified in the template did not exist\.  | 
| ProvisionThing\.ServerError |  The number of times a device failed to provision due to a server error\. Customers can retry to provision the device after waiting and they can contact AWS IoT if the issue remains the same\.  | 
| ProvisionThing\.Success |  The number of times a device was successfully provisioned\.  | 

## Fleet indexing metrics<a name="fleet-indexing-metrics"></a>


**AWS IoT fleet indexing metrics**  

| Metric | Description | 
| --- | --- | 
|  `NamedShadowCountForDynamicGroupQueryLimitExceeded`  |  A maximum of 25 named shadows per thing are processed for query terms that are not data source specific in dynamic thing groups\. When this limit is breached for a thing, the `NamedShadowCountForDynamicGroupQueryLimitExceeded` event type will be emitted\.  | 

## Dimensions for metrics<a name="aws-iot-metricdimensions"></a>


**Metrics use the namespace and provide metrics for the following dimensions**  

| Dimension | Description | 
| --- | --- | 
| ActionType |  The [action type](iot-rule-actions.md) specified by the rule that triggered the request\.  | 
|  `BehaviorName`  |  The name of the Device Defender Detect security profile behavior that is being monitored\.  | 
|  `ClaimCertificateId`  |  The `certificateId` of the claim used to provision the devices\.  | 
|  `CheckName`  |  The name of the Device Defender audit check whose results are being monitored\.  | 
|  `JobId`  |  The ID of the job whose progress or message connection success/failure is being monitored\.  | 
|  `Protocol`  |  The protocol used to make the request\. Valid values are: MQTT or HTTP  | 
|  `RuleName`  |  The name of the rule triggered by the request\.  | 
|  `ScheduledAuditName`  |  The name of the Device Defender scheduled audit whose check results are being monitored\. This has the value `OnDemand` if the results reported are for an audit that was performed on demand\.  | 
|  `SecurityProfileName`  |  The name of the Device Defender Detect security profile whose behaviors are being monitored\.  | 
|  `TemplateName`  |  The name of the provisioning template\.  | 