---
title: 還原 HDFS 管理員權限
titleSuffix: SQL Server Big Data Cluster
description: 還原 HDFS 管理員權限。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 04/21/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6fb8c7c53c6edf4a02649f256ac6aa6d7080fdf5
ms.sourcegitcommit: 1f9fc7402b00b9f35e02d5f1e67cad2f5e66e73a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82108692"
---
# <a name="restore-hdfs-admin-rights"></a>還原 HDFS 管理員權限

HDFS 存取控制清單 (ACL) 修改可能已影響 HDFS 中的 `/system` 和 `/tmp` 資料夾。 最有可能的 ACL 修改原因是使用者手動操作資料夾 ACL。 系統不支援直接修改 /system 資料夾與 /tmp/logs 資料夾中的權限。

## <a name="symptom"></a>徵狀

提交 Spark 作業時是透過 ADS，並且因 SparkContext 初始化錯誤和 AccessControlException 而失敗。

```
583 ERROR spark.SparkContext: Error initializing SparkContext.
org.apache.hadoop.security.AccessControlException: Permission denied: user=<UserAccount>, access=WRITE, inode="/system/spark-events":sph:BDCAdmin:drwxr-xr-x
```

Yarn UI 會顯示處於 KILLED 狀態的應用程式識別碼。

當您嘗試以網域使用者的身分寫入資料夾時，也會失敗。 您可以使用下列範例來進行測試：

```bash
kinit <UserAccount>
hdfs dfs -touch /system/spark-events/test
hdfs dfs -rm /system/spark-events/test
```

## <a name="cause"></a>原因

已針對 BDC 使用者網域安全性群組修改 HDFS ACL。 可能的修改包括 /system 和 /tmp 資料夾的 ACL。 系統不支援修改這些資料夾。

在 Livy 記錄檔中確認該效果：

```
INFO utils.LineBufferedStream: YYYY-MM-DD-HH:MM:SS,858 INFO yarn.Client: Application report for application_1580771254352_0041 (state: ACCEPTED)
...
WARN rsc.RSCClient: Client RPC channel closed unexpectedly.
INFO interactive.InteractiveSession: Failed to ping RSC driver for session <ID>. Killing application
```

YARN UI 會針對該應用程式識別碼顯示處於 KILLED 狀態的應用程式。

若要取得 RPC 連線關閉的根本原因，請檢查 YARN 應用程式記錄檔，以找出與該應用程式對應的應用程式。 在上述範例中，係指 `application_1580771254352_0041`。 使用 `kubectl` 來連線到 sparkhead-0 Pod，然後執行此命令：

下列命令會查詢 YARN 記錄檔以找出該應用程式。

```bash
yarn logs -applicationId application_1580771254352_0041
```

在下方的結果中，已針對使用者拒絕權限。 

```
YYYY-MM-DD-HH:MM:SS,583 ERROR spark.SparkContext: Error initializing SparkContext.
org.apache.hadoop.security.AccessControlException: Permission denied: user=user1, access=WRITE, inode="/system/spark-events":sph:BDCAdmin:drwxr-xr-x
```

原因可能是 BDC 使用者被以遞迴方式新增至 HDFS 根資料夾。 這可能已影響預設權限。

## <a name="resolution"></a>解決方案

請使用下列指令碼來還原權限：使用 `kinit` 搭配 admin：

```bash
hdfs dfs -chmod 733 /system/spark-events
hdfs dfs -setfacl --set default:user:sph:rwx,default:other::--- /system/spark-events
hdfs dfs -setfacl --set default:user:app-setup:r-x,default:other::--- /system/appdeploy
hadoop fs -chmod 733 /tmp/logs
hdfs dfs -setfacl --set default:user:yarn:rwx,default:other::--- /tmp/logs
```
