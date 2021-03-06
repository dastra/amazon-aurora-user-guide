# Enabling Performance Insights<a name="USER_PerfInsights.Enabling"></a>

To use Performance Insights, you must enable it on your DB instance\.

If you use Performance Insights together with Aurora Global Database, you must enable Performance Insights individually for the DB instances in each AWS Region\. For details, see [Performance Insights for Aurora Global Databases](aurora-global-database-managing.md#aurora-global-database-pi)\. 

The Performance Insights agent consumes limited CPU and memory on the DB host\. When the DB load is high, the agent limits the performance impact by collecting data less frequently\.

## Console<a name="USER_PerfInsights.Enabling.Console"></a>

You can use the console to enable Performance Insights when you create a new DB instance\. You can also modify a DB instance to enable Performance Insights\.

### Enabling Performance Insights with the Console When Creating a DB Instance<a name="USER_PerfInsights.Console.Creating"></a>

When you create a new DB instance, Performance Insights is enabled when you choose **Enable Performance Insights** in the **Performance Insights** section\.

To create a DB instance, follow the instructions for your DB engine in [Creating an Amazon Aurora DB Cluster](Aurora.CreateInstance.md)\.

The following screenshot shows the **Performance Insights** section\.

![\[Enable Performance Insights during DB instance creation with console\]](http://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/images/perf_insights_enabling.png)

You have the following options when you choose **Enable Performance Insights**:
+ **Retention** – The amount of time to retain Performance Insights data\. Choose either 7 days \(the default\) or 2 years\.
+ **Master key** – Specify your AWS Key Management Service \(AWS KMS\) key\. Performance Insights encrypts all potentially sensitive data using your AWS KMS key\. Data is encrypted in flight and at rest\. For more information, see [Encrypting Amazon Aurora Resources](Overview.Encryption.md)\.

### Enabling Performance Insights with the Console When Modifying a DB Instance<a name="USER_PerfInsights.Enabling.Console.Modifying"></a>

You can modify a DB instance to enable Performance Insights using the console\.

**To enable Performance Insights for a DB instance using the console**

1. Sign in to the AWS Management Console and open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Choose the DB instance that you want to modify, and choose **Modify**\.

1. In the **Performance Insights** section, choose **Enable Performance Insights**\.

   You have the following options when you choose **Enable Performance Insights**:
   + **Retention** – The amount of time to retain Performance Insights data\. Choose either 7 days \(the default\) or 2 years\.
   + **Master key** – Specify your AWS Key Management Service \(AWS KMS\) key\. Performance Insights encrypts all potentially sensitive data using your AWS KMS key\. Data is encrypted in flight and at rest\. For more information, see [Encrypting Amazon Aurora Resources](Overview.Encryption.md)\.

1. Choose **Continue**\.

1. For **Scheduling of Modifications**, choose one of the following:
   + **Apply during the next scheduled maintenance window** – Wait to apply the **Performance Insights** modification until the next maintenance window\.
   + **Apply immediately** – Apply the **Performance Insights** modification as soon as possible\.

1. Choose **Modify instance**\.

## AWS CLI<a name="USER_PerfInsights.Enabling.CLI"></a>

When you create a new DB instance using the [create\-db\-instance](https://docs.aws.amazon.com/cli/latest/reference/rds/create-db-instance.html) AWS CLI command, Performance Insights is enabled when you specify `--enable-performance-insights`\. 

You can also specify the `--enable-performance-insights` value using the following AWS CLI commands:
+  [create\-db\-instance\-read\-replica](https://docs.aws.amazon.com/cli/latest/reference/rds/create-db-instance-read-replica.html) 
+  [modify\-db\-instance](https://docs.aws.amazon.com/cli/latest/reference/rds/modify-db-instance.html) 
+  [restore\-db\-instance\-from\-s3](https://docs.aws.amazon.com/cli/latest/reference/rds/restore-db-instance-from-s3.html) 

The following procedure describes how to enable Performance Insights for a DB instance using the AWS CLI\.

**To enable Performance Insights for a DB instance using the AWS CLI**
+ Call the [modify\-db\-instance](https://docs.aws.amazon.com/cli/latest/reference/rds/modify-db-instance.html) AWS CLI command and supply the following values:
  + `--db-instance-identifier` – The name of the DB instance\.
  + `--enable-performance-insights`

  The following example enables Performance Insights for `sample-db-instance`\.

  For Linux, macOS, or Unix:

  ```
  aws rds modify-db-instance \
      --db-instance-identifier sample-db-instance \
      --enable-performance-insights
  ```

  For Windows:

  ```
  aws rds modify-db-instance ^
      --db-instance-identifier sample-db-instance ^
      --enable-performance-insights
  ```

When you enable Performance Insights, you can optionally specify the amount of time, in days, to retain Performance Insights data with the `--performance-insights-retention-period` option\. Valid values are 7 \(the default\) or 731 \(2 years\)\.

The following example enables Performance Insights for `sample-db-instance` and specifies that Performance Insights data is retained for two years\.

For Linux, macOS, or Unix:

```
aws rds modify-db-instance \
    --db-instance-identifier sample-db-instance \
    --enable-performance-insights \
    --performance-insights-retention-period 731
```

For Windows:

```
aws rds modify-db-instance ^
    --db-instance-identifier sample-db-instance ^
    --enable-performance-insights ^
    --performance-insights-retention-period 731
```

## RDS API<a name="USER_PerfInsights.Enabling.API"></a>

When you create a new DB instance using the [CreateDBInstance](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_CreateDBInstance.html) operation Amazon RDS API operation, Performance Insights is enabled when you set `EnablePerformanceInsights` to `True`\. 

You can also specify the `EnablePerformanceInsights` value using the following API operations:
+  [ModifyDBInstance](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_ModifyDBInstance.html) 
+  [CreateDBInstanceReadReplica](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_CreateDBInstanceReadReplica.html) 
+  [RestoreDBInstanceFromS3](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_RestoreDBInstanceFromS3.html) 

When you enable Performance Insights, you can optionally specify the amount of time, in days, to retain Performance Insights data with the `PerformanceInsightsRetentionPeriod` parameter\. Valid values are 7 \(the default\) or 731 \(2 years\)\.

## Enabling the Performance Schema for Performance Insights on Aurora MySQL<a name="USER_PerfInsights.EnableMySQL"></a>

When the Performance Schema feature is enabled for Aurora MySQL, Performance Insights provides more detailed information\. For example, Performance Insights displays DB load categorized by detailed wait events\. Without the Performance Schema enabled, Performance Insights displays DB load categorized by the list state of the MySQL process\.

The Performance Schema is enabled automatically when you create an Aurora MySQL DB instance with Performance Insights enabled\. In this case, Performance Insights automatically manages the parameters in the following table\.

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/USER_PerfInsights.Enabling.html)

**Important**  
When Performance Schema is enabled automatically, Performance Insights changes schema\-related parameters on the DB instance\. These changes aren't visible in the parameter group associated with the DB instance\.