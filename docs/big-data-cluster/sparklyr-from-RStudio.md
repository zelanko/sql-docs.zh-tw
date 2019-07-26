---
title: 使用 RStudio 的 sparklyr
titleSuffix: SQL Server big data clusters
description: 使用 RStudio 的 sparklyr 連接到 big data cluster。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f346fed17e4c79214a7eba43f70767fc80b98a07
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67728381"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>在 SQL Server big data cluster 中使用 sparklyr

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr 提供 Apache Spark 的 R 介面。 Sparklyr 是讓 R 開發人員使用 Spark 的熱門方式。 本文說明如何在使用 RStudio 的 SQL Server 2019 big data cluster (預覽) 中使用 sparklyr。

## <a name="prerequisites"></a>先決條件

- [部署 SQL Server 2019 big data](quickstart-big-data-cluster-deploy.md)叢集。

### <a name="install-rstudio-desktop"></a>安裝 RStudio Desktop

使用下列步驟安裝及設定**RStudio Desktop** :

1. 如果您是在 Windows 用戶端上執行, 請[下載並安裝 R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4)。

1. [下載並安裝 RStudio Desktop](https://www.rstudio.com/products/rstudio/download/)。

1. 安裝完成之後, 請在 RStudio Desktop 內執行下列命令, 以安裝必要的套件:

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>連接到大型資料叢集中的 Spark

您可以使用 sparklyr, 從用戶端連接到使用 Livy 和 HDFS/Spark 閘道的 big data 叢集。 

在 RStudio 中, 建立 R 腳本並連接至 Spark, 如下列範例所示:

> [!TIP]
> `<USERNAME>`針對和`<PASSWORD>`值, 請使用您在 big data cluster 部署期間所設定的使用者名稱 (例如 root) 和密碼。 如需`<PORT>`和值, 請參閱[連接到大型資料](connect-to-big-data-cluster.md)叢集的相關檔。 `<IP>`

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

連接到 Spark 之後, 您就可以執行 sparklyr。 下列範例會使用 sparklyr 在鳶尾花資料集上執行查詢:

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>分散式 R 計算

Sparklyr 的其中一項功能是能夠使用[spark_apply](https://spark.rstudio.com/reference/spark_apply/)來[散發 R 計算](https://spark.rstudio.com/guides/distributed-r/)。

因為 big data 叢集使用 Livy 連接, 所以您必須`packages = FALSE`在對**spark_apply**的呼叫中設定。 如需詳細資訊, 請參閱分散式 R 計算上 sparklyr 檔的[Livy 一節](https://spark.rstudio.com/guides/distributed-r/#livy)。 使用此設定時, 您只能在傳遞至**spark_apply**的 r 程式碼中, 使用已安裝在 Spark 叢集上的 r 套件。 下列範例示範這項功能:

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>後續步驟

如需 big data 叢集的詳細資訊, 請參閱[什麼是 SQL Server 2019 big data](big-data-cluster-overview.md)叢集。
