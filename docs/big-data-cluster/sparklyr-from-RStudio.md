---
title: 從 RStudio 使用 sparklyr
titleSuffix: SQL Server big data clusters
description: 從 RStudio 使用 sparklyr 連接到巨量資料叢集。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 375993e4fd9506c129e4f98d9ad2193472e03edb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "73531621"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>在 SQL Server 巨量資料叢集中使用 sparklyr

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

sparklyr 提供適用於 Apache Spark 的 R 介面。 sparklyr 是 R 開發人員使用 Spark 的一種常見方式。 本文描述如何使用 RStudio 在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 中使用 sparklyr。

## <a name="prerequisites"></a>Prerequisites

- [部署 SQL Server 2019 巨量資料叢集](quickstart-big-data-cluster-deploy.md)。

### <a name="install-rstudio-desktop"></a>安裝 RStudio Desktop

使用下列步驟來安裝和設定 **RStudio Desktop**：

1. 如果您是在 Windows 用戶端上執行，請[下載並安裝 R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4)。

1. [下載並安裝 RStudio Desktop](https://www.rstudio.com/products/rstudio/download/)。

1. 安裝完成之後，請在 RStudio Desktop 內執行下列命令，以安裝必要的套件：

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>連接至巨量資料叢集中的 Spark

您可以使用 sparklyr，從用戶端連接到使用 Livy 和 HDFS/Spark 閘道的巨量資料叢集。 

在 RStudio 中，建立 R 指令碼並連接至 Spark，如下列範例所示：

> [!TIP]
> 針對 `<AZDATA_USERNAME>` 和 `<AZDATA_PASSWORD>` 值，請使用您在巨量資料叢集部署期間所設定的使用者名稱 (例如 root) 和密碼。 針對 `<IP>` 和 `<PORT>` 值，請參閱[連接到巨量資料叢集](connect-to-big-data-cluster.md)的相關文件。

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "<AZDATA_USERNAME>", password = "<AZDATA_PASSWORD>")

httr::set_config(httr::config(ssl_verifypeer = 0L, ssl_verifyhost = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>執行 sparklyr 查詢

連接到 Spark 之後，您就可以執行 sparklyr。 下列範例會使用 sparklyr 在 Iris 資料集上執行查詢：

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>分散式 R 計算

sparklyr 的其中一項功能，就是能夠使用 [spark_apply](https://spark.rstudio.com/reference/spark_apply/) 來[散發 R 計算](https://spark.rstudio.com/guides/distributed-r/)。

因為巨量資料叢集使用 Livy 連線，所以您必須將呼叫中的 `packages = FALSE` 設定為 **spark_apply**。 如需詳細資訊，請參閱分散式 R 計算相關 sparklyr 文件的 [Livy 一節](https://spark.rstudio.com/guides/distributed-r/#livy)。 使用此設定時，您只能在要傳遞給 **spark_apply** 的 R 程式碼中使用 Spark 叢集上所安裝 R 套件。 下列範例示範此功能：

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)。
