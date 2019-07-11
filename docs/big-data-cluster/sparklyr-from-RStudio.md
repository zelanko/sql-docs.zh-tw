---
title: 使用 RStudio 從 sparklyr
titleSuffix: SQL Server big data clusters
description: 連接到使用 RStudio 從 sparklyr 的巨量資料叢集。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f346fed17e4c79214a7eba43f70767fc80b98a07
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728381"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>在 SQL Server 巨量資料叢集中使用 sparklyr

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr 提供適用於 Apache Spark 的 R 介面。 Sparklyr 是使用 Spark 的 R 開發人員的熱門方式。 本文說明如何使用 sparklyr 使用 RStudio 的 SQL Server 2019 巨量資料叢集 （預覽）。

## <a name="prerequisites"></a>必要條件

- [部署 SQL Server 2019 巨量資料叢集](quickstart-big-data-cluster-deploy.md)。

### <a name="install-rstudio-desktop"></a>安裝 RStudio Desktop

安裝和設定**RStudio Desktop**進行下列步驟：

1. 如果您執行 Windows 用戶端上[下載並安裝 R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4)。

1. [下載並安裝 RStudio Desktop](https://www.rstudio.com/products/rstudio/download/)。

1. 安裝完成後，執行下列命令以安裝必要的套件內 RStudio Desktop:

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>連線到 Spark 中的巨量資料叢集

您可以從用戶端連線到使用 Livy 與 HDFS/Spark 閘道的巨量資料叢集使用 sparklyr。 

在 RStudio 中，建立 R 指令碼，並連線至 Spark，如下列範例所示：

> [!TIP]
> 針對`<USERNAME>`和`<PASSWORD>`值，會使用 （例如根） 的使用者名稱和您在巨量資料叢集部署期間設定的密碼。 針對`<IP>`並`<PORT>`的值，請參閱文件[連線到巨量資料叢集](connect-to-big-data-cluster.md)。

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
