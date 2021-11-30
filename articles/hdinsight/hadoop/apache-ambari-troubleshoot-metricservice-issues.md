---
title: Apache Ambari Metrics Collector issues in Azure HDInsight
description: Troubleshooting Apache Ambari Metrics Collector issues in Azure HDInsight
ms.service: hdinsight
ms.author: linjzhu
author: jacky-hdi
ms.topic: troubleshooting
ms.date: 11/03/2021
---

# Apache Ambari Metrics Collector issues in Azure HDInsight

This article describes troubleshooting steps and possible resolutions for issues when interacting with Azure HDInsight clusters.

## Scenario: OutOfMemoryError or Unresponsive Apache Ambari Metrics Collector

### Issue

* You could receive a critical **"Metrics Collector Process"** alert in Ambari UI and show below similar message.
    `Connection failed: timed out to <headnode fqdn>:6188`
* Ambari Metrics Collector maybe getting restarted in the headnode frequently
* Some Apache Ambari metrics may not show up. For example, **NAMENODE** shows **Started** instead of **Active/Standby** status 


### Cause

The following scenarios are possible causes of these issues:

#### An out of memory exception happens frequently

Check the Apache Ambari Metrics Collector log `/var/log/ambari-metrics-collector/ambari-metrics-collector.log*`.

```
19:59:45,457 ERROR [325874797@qtp-2095573052-22] log:87 - handle failed
java.lang.OutOfMemoryError: Java heap space

19:59:45,457 FATAL [MdsLoggerSenderThread] YarnUncaughtExceptionHandler:51 - Thread Thread[MdsLoggerSenderThread,5,main] threw an Error.  Shutting down now...
java.lang.OutOfMemoryError: Java heap space
```

#### Busy garbage collection

1. Apache Ambari Metrics Collector is not listening on **6188** in hbase-ams log `/var/log/ambari-metrics-collector/hbase-ams-master-hn*.log`

   ```
   2021-04-13 05:57:37,546 INFO  [timeline] timeline.HadoopTimelineMetricsSink: No live collector to send metrics to. Metrics to be sent will be discarded. This message will be skipped for the next 20 times.
   ```
   
2. Get the Apache Ambari Metrics Collector pid and check GC performance

   ```
   ps -fu ams | grep 'org.apache.ambari.metrics.AMSApplicationServer'
   ```
       
3. Check the garbage collection status using `jstat -gcutil <pid> 1000 100`. If you see the **FGCT** increase a lot in short seconds, it indicates Apache Ambari Metrics Collector is busy in Full GC and unable to process the other requests.

### Resolution

To avoid these issues, consider using one of the following options:

1. Increase the heap memory of Apache Ambari Metrics Collector from **Ambari** > **Ambari Metric Collector** > **Configuration** > **Metrics Collector Heap Size**

   :::image type="content" source="./media/apache-ambari-troubleshoot-ams-issues/editing-ams-configuration-ambari.png" alt-text="Screenshot of editing Ambari Metric Service configuration properties." border="true":::

2. Follow these steps to clean up Ambari Metrics service (AMS) data.

   > [!NOTE]
   > Cleaning up the AMS data removes all the historical AMS data available. If you need the history, this may not be the best option.

   1.  Login into the Ambari portal  
	1.  Set AMS to maintenance  
	2.  Stop AMS from Ambari  
	3.  Identify the following from the **AMS Configs** screen  
            	1.  `hbase.rootdir` (Default value is `file:///mnt/data/ambari-metrics-collector/hbase`)  
            	2.  `hbase.tmp.dir`(Default value is `/var/lib/ambari-metrics-collector/hbase-tmp`)  
   2. SSH into headnode where Apache Ambari Metrics Collector exists. As superuser:
	1. Remove the AMS zookeeper data by **backing up** and removing the contents of  `'hbase.tmp.dir'/zookeeper`
	2. Remove any Phoenix spool files from `<hbase.tmp.dir>/phoenix-spool` folder 
	3. ***(It is worthwhile to skip this step initially and try restarting AMS to see if the issue is resolved. If AMS is still failing to come up, try this step)***  
	    	AMS data would be stored in `hbase.rootdir` identified above. Use regular OS commands to back up and remove the files. Example:  	
        	`tar czf /mnt/backupof-ambari-metrics-collector-hbase-$(date +%Y%m%d-%H%M%S).tar.gz /mnt/data/ambari-metrics-collector/hbase`  
   3.  Restart AMS using Ambari.


## Next steps

[!INCLUDE [troubleshooting next steps](../includes/hdinsight-troubleshooting-next-steps.md)]
