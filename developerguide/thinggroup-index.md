# Manage thing group indexing<a name="thinggroup-index"></a>

`AWS_ThingGroups` is the index that contains all of your thing groups\. You can use this index to search for groups based on group name, description, attributes, and all parent group names\.

## Enabling thing group indexing<a name="enable-group-index"></a>

You can use the `thing-group-indexing-configuration` setting in the [UpdateIndexingConfiguration](https://docs.aws.amazon.com/iot/latest/apireference/API_UpdateIndexingConfiguration.html) API to create the `AWS_ThingGroups` index and control its configuration\. You can use the [GetIndexingConfiguration](https://docs.aws.amazon.com/iot/latest/apireference/API_GetIndexingConfiguration.html) API to retrieve the current indexing configuration\. 

To update the thing group indexing configurations, run the update\-indexing\-configuration CLI command:

```
aws iot update-indexing-configuration --thing-group-indexing-configuration thingGroupIndexingMode=ON
```

You can also update configurations for both thing and thing group indexing in a single command, as follows:

```
aws iot update-indexing-configuration --thing-indexing-configuration thingIndexingMode=REGISTRY --thing-group-indexing-configuration thingGroupIndexingMode=ON
```

The following are valid values for `thingGroupIndexingMode`\.

OFF  
No indexing/delete index\.

ON  
Create or configure the `AWS_ThingGroups` index\.

To retrieve the current thing and thing group indexing configurations, run the get\-indexing\-configuration CLI command:

```
aws iot get-indexing-configuration
```

The response of the command looks like the following:

```
{
   "thingGroupIndexingConfiguration": {
        "thingGroupIndexingMode": "ON"
    }
}
```

## Describing group indexes<a name="describe-group-index"></a>

To retrieve the current status of the `AWS_ThingGroups` index, use the describe\-index CLI command:

```
aws iot describe-index --index-name "AWS_ThingGroups"
```

The response of the command looks like the following:

```
{
   "indexStatus": "ACTIVE", 
   "indexName": "AWS_ThingGroups", 
   "schema": "THING_GROUPS"
}
```

 AWS IoT builds your index the first time you enable indexing\. You can't query the index if the `indexStatus` is `BUILDING`\.

## Querying a thing group index<a name="search-group-index"></a>

To query data in the index, use the search\-index CLI command:

```
aws iot search-index --index-name "AWS_ThingGroups" --query-string "thingGroupName:mythinggroup*"
```

## Authorization<a name="query-thinggroup-auth"></a>

You can specify the thing groups index as a resource ARN in an AWS IoT policy action, as follows\.


****  

| Action | Resource | 
| --- | --- | 
|  `iot:SearchIndex`  |  An index ARN \(for example, `arn:aws:iot:your-aws-region:index/AWS_ThingGroups`\)\.  | 
|  `iot:DescribeIndex`  |  An index ARN \(for example, `arn:aws:iot:your-aws-region:index/AWS_ThingGroups`\)\.  | 