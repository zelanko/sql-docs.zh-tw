---
title: Apache Spark 和 Apache Hadoop
titleSuffix: Configure Apache Spark and Apache Hadoop in Big Data Clusters
description: SQL Server 巨量資料叢集允許 Spark 和 HDFS 解決方案。 了解其設定方法。
author: rajmera3
ms.author: raajmera
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1e5d0941256fbb1e167f65489e250eed9c9b895a
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257218"
---
# <a name="configure-apache-spark-and-apache-hadoop-in-big-data-clusters"></a>在巨量資料叢集中設定 Apache Spark 和 Apache Hadoop

為了在巨量資料叢集中設定 Apache Spark 和 Apache Hadoop，您必須在部署階段修改叢集設定檔。

巨量資料叢集有四個組態類別： 

- `sql` 
- `hdfs` 
- `spark` 
- `gateway` 

`sql`、`hdfs`、`spark`、`sql` 為服務。 每項服務都會對應到同名的組態類別。 所有閘道組態都會分在 `gateway` 類別。 

例如，服務 `hdfs` 中的所有組態都屬於 `hdfs` 類別。 請注意，所有 Hadoop (核心網站)、HDFS 和 Zookeeper 組態都屬於 `hdfs` 類別，而所有 Livy、Spark、Yarn、Hive 中繼存放區組態都屬於 `spark` 類別。 

[支援的設定](reference-config-spark-hadoop.md#supported-configurations)會列出您可以在部署 SQL Server 巨量資料叢集時設定的 Apache Spark 與 Hadoop 屬性。

下列各節列出您在叢集中**無法**修改的屬性：

- [不支援的 `spark` 設定](reference-config-spark-hadoop.md#unsupported-spark-configurations)
- [不支援的 `hdfs` 設定](reference-config-spark-hadoop.md#unsupported-hdfs-configurations)
- [不支援的 `gateway` 設定](reference-config-spark-hadoop.md#unsupported-gateway-configurations)


## <a name="configurations-via-cluster-profile"></a>透過叢集設定檔進行設定

在叢集設定檔中有資源和服務。 在部署階段，我們可以使用下列兩種方式之一來指定組態： 

* 第一種，在資源層級： 

   下列範例是設定檔的修補檔案： 

   ```json
   { 
         "op": "add", 
         "path": "spec.resources.zookeeper.spec.settings", 
         "value": { 
           "hdfs": { 
             "zoo-cfg.syncLimit": "6" 
           } 
         } 
   }
   ```

   或： 

   ```json
   { 
         "op": "add", 
         "path": "spec.resources.gateway.spec.settings", 
         "value": { 
           "gateway": { 
             "gateway-site.gateway.httpclient.socketTimeout": "95s" 
           } 
         } 
   } 
   ```

* 第二種，在服務層級。 將多種資源指派給某項服務，並指定服務的組態。

下列為設定 HDFS 區塊大小所用設定檔的修補檔案範例： 

   ```json
   { 
         "op": "add", 
         "path": "spec.services.hdfs.settings", 
         "value": { 
           "hdfs-site.dfs.block.size": "268435456" 
        } 
   } 
   ```

服務 `hdfs` 定義如下：

```json
{ 
  "spec": { 
   "services": { 
     "hdfs": { 
        "resources": [ 
          "nmnode-0", 
          "zookeeper", 
          "storage-0", 
          "sparkhead" 
        ], 
        "settings":{ 
          "hdfs-site.dfs.block.size": "268435456" 
        } 
      } 
    } 
  } 
} 
```
 
> [!NOTE]
> 資源層級組態會覆寫服務層級組態。 一種資源可以指派給多項服務。

## <a name="enable-spark-in-the-storage-pool"></a>在存放集區中啟用 Spark
除了支援的 Apache 設定之外，我們還提供設定 Spark 作業是否可在存放集區中執行的功能。 `includeSpark` 這個布林值位於 `spec.resources.storage-0.spec.settings.spark` 的 `bdc.json` 組態檔中。

bdc.json 中的範例存放集區定義可能如下所示：
```json
...
"storage-0": {
                "metadata": {
                    "kind": "Pool",
                    "name": "default"
                },
                "spec": {
                    "type": "Storage",
                    "replicas": 2,
                    "settings": {
                        "spark": {
                            "includeSpark": "true"
                        }
                    }
                }
            }
```


## <a name="limitations"></a>限制

只能在類別層級指定組態。 若要指定多個具有相同子類別的組態，我們無法在叢集設定檔中解壓縮共同首碼。 

```json
{ 
      "op": "add", 
      "path": "spec.services.hdfs.settings.core-site.hadoop", 
      "value": { 
        “proxyuser.xyz.users”: “*”, 
        “proxyuser.abc.users”: “*” 
     } 
} 
```

## <a name="next-steps"></a>後續步驟

- [Apache Spark 與 Apache Hadoop (HDFS) 設定屬性。](reference-config-spark-hadoop.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 參考](../azdata/reference/reference-azdata.md)
- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)