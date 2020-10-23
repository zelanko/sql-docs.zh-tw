---
title: 針對 `pyspark` 筆記本進行疑難排解
titleSuffix: SQL Server Big Data Cluster
description: 針對 `pyspark` 筆記本進行疑難排解
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mikeray
ms.date: 06/01/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d631a74bc71c814a70ef0ecfa33485ee4631ccd4
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257070"
---
# <a name="troubleshoot-pyspark-notebook"></a>針對 `pyspark` 筆記本進行疑難排解

本文示範如何針對失敗的 `pyspark` 筆記本進行疑難排解。

## <a name="architecture-of-a-pyspark-job-under-azure-data-studio"></a>Azure Data Studio 下的 PySpark 作業架構

Azure Data Studio 與 SQL Server BDC 上的 `livy` 端點通訊。 

`livy` 端點會在 BDC 叢集中發出 `spark-submit` 命令。 每個 `spark-submit` 命令都有一個參數，其可將 YARN 指定為叢集資源管理員。

若要有效率地針對 PySpark 工作階段進行疑難排解，則必須收集及檢閱每一層中的記錄：Livy、YARN 與 Spark。

此疑難排解步驟需要具備：

1. 已安裝 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]，且已將組態正確地設定為叢集。
2. 熟悉執行 Linux 命令及一些記錄疑難排解技能。

## <a name="troubleshooting-steps"></a>疑難排解步驟

1. 請檢閱 `pyspark` 中的堆疊與錯誤訊息。

   從筆記本中的第一個資料格取得應用程式識別碼。 使用此應用程式識別碼來調查 `livy`、YARN 與 Spark 記錄。 `SparkContext` 則使用此 YARN 應用程式識別碼。

   :::image type="content" source="../big-data-cluster/media/troubleshoot-pyspark-notebook/1-failed-cell.png" alt-text="失敗的資料格":::

1. 取得記錄。

   使用 `azdata bdc debug copy-logs` 調查

   下列範例會連線巨量資料叢集端點，以複製記錄。 在執行之前，請先更新下列範例中的值。
   - `<ip_address>`:巨量資料叢集端點
   - `<username>`:巨量資料叢集名稱
   - `<namespace>`:叢集的 Kubernetes 命名空間
   - `<folder_to_copy_logs>`:您想要將記錄複製到其中的本機資料夾路徑

   ```console
   azdata login --auth basic --username <username> --endpoint https://<ip_address>:30080
   azdata bdc debug copy-logs -n <namespace> -d <folder_to_copy_logs>
   ```

   範例輸出

   ```output
   <user>@<server>:~$ azdata bdc debug copy-logs -n <namespace> -d copy_logs
   Collecting the logs for cluster '<namespace>'.
   Collecting logs for containers...
   Creating an archive from logs-tmp/<namespace>.
   Log files are archived in /home/<user>/copy_logs/debuglogs-<namespace>-YYYYMMDD-HHMMSS.tar.gz.
   Creating an archive from logs-tmp/dumps.
   Log files are archived in /home/<user>/copy_logs/debuglogs-<namespace>-YYYYMMDD-HHMMSS-dumps.tar.gz.
   Collecting the logs for cluster 'kube-system'.
   Collecting logs for containers...
   Creating an archive from logs-tmp/kube-system.
   Log files are archived in /home/<user>/copy_logs/debuglogs-kube-system-YYYYMMDD-HHMMSS.tar.gz.
   Creating an archive from logs-tmp/dumps.
   Log files are archived in /home/<user>/copy_logs/debuglogs-kube-system-YYYYMMDD-HHMMSS-dumps.tar.gz.
   ```

1. 檢閱 Livy 記錄。 Livy 記錄在 `<namespace>\sparkhead-0\hadoop-livy-sparkhistory\supervisor\log`。

   - 從 pyspark 筆記本的第一個儲存格搜尋 YARN 應用程式識別碼。
   - 搜尋 `ERR` 狀態。
   
   具有 `YARN ACCEPTED` 狀態的 Livy 記錄範例。 Livy 已提交 Yarn 應用程式。

   ```output
   HH:MM:SS INFO utils.LineBufferedStream: YYY-MM-DD HH:MM:SS INFO impl.YarnClientImpl: Submitted application application_<application_id>
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream: YYY-MM-DD HH:MM:SS INFO yarn.Client: Application report for application_<application_id> (state: ACCEPTED)
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream: YYY-MM-DD HH:MM:SS INFO yarn.Client: 
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      client token: N/A
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      diagnostics: N/A
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      ApplicationMaster host: N/A
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      ApplicationMaster RPC port: -1
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      queue: default
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      start time: ############
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      final status: UNDEFINED
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      tracking URL: https://sparkhead-1.fnbm.corp:8090/proxy/application_<application_id>/
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      user: <account>
   ```

1. 檢閱 Yarn UI

   從 Azure Data Studio 巨量資料叢集管理儀表板取得 YARN 端點 URL，或執行 `azdata bdc endpoint list –o table`。

   例如：

   ```console
   azdata bdc endpoint list -o table
   ```

   傳回值

   ```output
   Description                                             Endpoint                                                          Name                        Protocol
   ------------------------------------------------------  ----------------------------------------------------------------  --------------------------  ----------
   Gateway to access HDFS files, Spark                     https://knox.<namespace-value>.local:30443                               gateway                     https
   Spark Jobs Management and Monitoring Dashboard          https://knox.<namespace-value>.local:30443/gateway/default/sparkhistory  spark-history               https
   Spark Diagnostics and Monitoring Dashboard              https://knox.<namespace-value>.local:30443/gateway/default/yarn          yarn-ui                     https
   Application Proxy                                       https://proxy.<namespace-value>.local:30778                              app-proxy                   https
   Management Proxy                                        https://bdcmon.<namespace-value>.local:30777                             mgmtproxy                   https
   Log Search Dashboard                                    https://bdcmon.<namespace-value>.local:30777/kibana                      logsui                      https
   Metrics Dashboard                                       https://bdcmon.<namespace-value>.local:30777/grafana                     metricsui                   https
   Cluster Management Service                              https://bdcctl.<namespace-value>.local:30080                             controller                  https
   SQL Server Master Instance Front-End                    sqlmaster.<namespace-value>.local,31433                                  sql-server-master           tds
   SQL Server Master Readable Secondary Replicas           sqlsecondary.<namespace-value>.local,31436                               sql-server-master-readonly  tds
   HDFS File System Proxy                                  https://knox.<namespace-value>.local:30443/gateway/default/webhdfs/v1    webhdfs                     https
   Proxy for running Spark statements, jobs, applications  https://knox.<namespace-value>.local:30443/gateway/default/livy/v1       livy                        https
   ```

1. 檢查應用程式識別碼與個別 application_master 與容器記錄。

   :::image type="content" source="media/troubleshoot-pyspark-notebook/15-hadoop-dashboard.png" alt-text="失敗的資料格":::

1. 檢閱 YARN 應用程式記錄檔。

   取得應用程式的應用程式記錄檔。 使用 `kubectl` 連線至 `sparkhead-0` Pod，例如：
   
   ```console
   kubectl exec -it sparkhead-0 -- /bin/bash
   ```
      
   然後使用正確的 `application_id`，在該殼層中執行此命令：

   ```console
   yarn logs -applicationId application_<application_id>
   ```

1. 搜尋錯誤或堆疊。

   HDFS 的權限錯誤範例。 在 Java 堆疊中，尋找 `Caused by:`

   ```output
   YYYY-MM-DD HH:MM:SS,MMM ERROR spark.SparkContext: Error initializing SparkContext.
   org.apache.hadoop.security.AccessControlException: Permission denied: user=<account>, access=WRITE, inode="/system/spark-events":sph:<bdc-admin>:drwxr-xr-x
        at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.check(FSPermissionChecker.java:399)
        at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:255)
        at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:193)
        at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1852)
        at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1836)
        at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkAncestorAccess(FSDirectory.java:1795)
        at org.apache.hadoop.hdfs.server.namenode.FSDirWriteFileOp.resolvePathForStartFile(FSDirWriteFileOp.java:324)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.startFileInt(FSNamesystem.java:2504)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.startFileChecked(FSNamesystem.java:2448)
   
   Caused by: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.security.AccessControlException): Permission denied: user=<account>, access=WRITE, inode="/system/spark-events":sph:<bdc-admin>:drwxr-xr-x
   ```

1. 檢閱 SPARK UI。

   :::image type="content" source="media/troubleshoot-pyspark-notebook/30-spark-ui.png" alt-text="失敗的資料格":::

   向下鑽研至尋找錯誤的階段工作。

## <a name="next-steps"></a>後續步驟

[針對 SQL Server 巨量資料叢集 Active Directory 整合進行疑難排解](troubleshoot-active-directory.md)