---
title: 使用 RStudio 從 sparklyr
titleSuffix: SQL Server big data clusters
description: 連接到使用 RStudio 從 sparklyr 的巨量資料叢集。
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 148e4942babafb35af2efe33eb427f9462f0a47e
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59969874"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>在 SQL Server 巨量資料叢集中使用 sparklyr

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr 提供適用於 Apache Spark 的 R 介面。 Sparklyr 是使用 Spark 的 R 開發人員的熱門方式。 本文說明如何使用 sparklyr 使用 RStudio 的 SQL Server 2019 巨量資料叢集 （預覽）。

## <a name="prerequisites"></a>先決條件

- [部署 SQL Server 2019 巨量資料叢集](quickstart-big-data-cluster-deploy.md)。

### <a name="install-rstudio-desktop"></a>安裝 RStudio Desktop

安裝和設定**RStudio Desktop**進行下列步驟：

1. 如果您執行 Windows 用戶端上[下載並安裝 R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4)。

1. [下載並安裝 RStudio Desktop](https://www.rstudio.com/products/rstudio/download/)。

1. 安裝完成後，執行下列命令以安裝必要的套件內 RStudio Desktop:

   ```RStudio Desktop install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01") install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01") install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## Connect to Spark in a big data cluster

You can use sparklyr to connect from a client to the big data cluster using Livy and the HDFS/Spark gateway. 

In RStudio, create an R script and connect to Spark as in the following example:

> [!TIP]
> For the `<USERNAME>` and `<PASSWORD>` values, use the username (such as root) and password you set during the big data cluster deployment. For the `<IP>` and `<PORT>` values, see the documentation on the [HDFS/Spark gateway](connect-to-big-data-cluster.md#hdfs).

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "<username>", password = "<password>")

httr::set_config(httr::config(ssl_verifypeer = 0L, ssl_verifyhost = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>執行 sparklyr 查詢

連接到 Spark 之後，您可以執行 sparklyr。 下列範例會使用 sparklyr 鳶尾花資料集上執行查詢：

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>分散式的 R 計算

Sparklyr 的其中一個功能是能夠[散發 R 計算](https://spark.rstudio.com/guides/distributed-r/)具有[spark_apply](https://spark.rstudio.com/reference/spark_apply/)。

巨量資料叢集使用 Livy 連線，因為您必須設定`packages = FALSE`的呼叫中**spark_apply**。 如需詳細資訊，請參閱 < [Livy 區段](https://spark.rstudio.com/guides/distributed-r/#livy)sparklyr 文件上分散式 R 計算。 使用此設定，您可以只使用傳遞至 R 程式碼中的 Spark 叢集已安裝的 R 封裝**spark_apply**。 下列範例會示範這項功能：

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>後續步驟

如需有關巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 2019 巨量資料叢集](big-data-cluster-overview.md)。