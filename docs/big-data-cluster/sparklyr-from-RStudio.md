---
title: 使用 RStudio 從 sparklyr
titleSuffix: SQL Server 2019 big data clusters
description: 連接到使用 RStudio 從 sparklyr 的巨量資料叢集。
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 83980f9d08a3894b0fbf7871cf899483e06702c4
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018354"
---
# <a name="use-sparklyr-in-sql-server-2019-big-data-cluster"></a>在 SQL Server 2019 巨量資料叢集使用 Sparklyr

Sparklyr 提供適用於 Apache Spark 的 R 介面。 Sparklyr 是使用 Spark 的 R 開發人員的慣用方式。 本文說明如何使用 sparklyr 使用 RStudio 的 SQL Server 2019 巨量資料叢集 （預覽）。

## <a name="prerequisites"></a>先決條件

- [部署 SQL Server 2019 巨量資料叢集](quickstart-big-data-cluster-deploy.md)。
- [安裝 RStudio](https://www.rstudio.com/)

## <a name="connect-to-spark-in-ss19-big-data-cluster"></a>連接到 spark 中 SS19 巨量資料叢集

在 RStudio 中建立 RScript 並連線至 Spark，如下所示。 Spark 巨量資料叢集連線透過 Livy，可使用連線[HDFS/Spark 閘道](connect-to-big-data-cluster.md#hdfs)。 進行驗證，使用使用者名稱和您在部署期間設定的密碼。

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "***root***", password = "****")

httr::set_config(httr::config(ssl_verifypeer = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>執行 sparklyr 查詢

連接到 Spark 之後，您可以執行 sparklyr。 下列範例會使用 sparklyr 鳶尾花資料集上執行查詢：

``` r
copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="next-steps"></a>後續步驟

如需有關巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。