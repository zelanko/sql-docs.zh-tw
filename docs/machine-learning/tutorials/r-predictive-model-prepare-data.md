---
title: 教學課程：準備在 R 中定型預測模型所需的資料
titleSuffix: SQL machine learning
description: 在這個四部分教學課程系列的第二部分中，您將準備資料，以使用 SQL 機器學習在 R 中定型預測模型。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: 55f416890794509f2fd141c2a907222a7d72c47e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470139"
---
# <a name="tutorial-prepare-data-to-train-a-predictive-model-in-r-with-sql-machine-learning"></a>教學課程：準備資料以使用 SQL 機器學習在 R 中定型預測模型
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
在這個四部分教學課程系列的第二部分中，您會使用 R 準備來自資料庫中的資料。在本系列稍後的內容中，您則會使用此資料透過 SQL Server 機器學習服務在 R 中定型和部署預測模型，或在巨量資料叢集上進行此定型和部署。
::: moniker-end
::: moniker range="=sql-server-2017"
在這個四部分教學課程系列的第二部分中，您會使用 R 準備來自資料庫中的資料。在本系列稍後的內容中，您則會使用此資料透過 SQL Server 機器學習服務在 R 中定型和部署預測模型。
::: moniker-end
::: moniker range="=sql-server-2016"
在這個四部分教學課程系列的第二部分中，您會使用 R 準備來自資料庫中的資料。在本系列稍後的內容中，您則會使用此資料透過 SQL Server R Services 在 R 中定型和部署預測模型。
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
在這個四部分教學課程系列的第二部分中，您會使用 R 來準備資料庫中的資料。在本系列稍後的內容中，您將透過 Azure SQL 受控執行個體機器學習服務，以使用此資料定型及部署 R 中的預測性模型。
::: moniker-end

在本文中，您將學會如何：

> [!div class="checklist"]
> * 將範例資料庫還原至資料庫
> * 將資料庫中的資料載入到 R 資料框架中
> * 藉由依某些資料行分類來以 R 準備資料

在[第一部分](r-predictive-model-introduction.md)，您已了解如何還原範例資料庫。

在[第三部分](r-predictive-model-train.md)中，您將了解如何在 R 中定型機器學習模型。

在[第四部分](r-predictive-model-deploy.md)中，您將了解如何將模型儲存在資料庫中，然後從您在第二和第三部分中開發的 R 指令碼建立預存程序。 預存程序將會在伺服器上中執行，以根據新資料進行預測。

## <a name="prerequisites"></a>Prerequisites

本教學課程的第二部分假設您已完成 [**第一部分**](r-predictive-model-introduction.md)及其必要條件。

## <a name="load-the-data-into-a-data-frame"></a>將資料載入資料框架

若要在 R 中使用資料，請將資料庫中的資料載入資料框架 (`rentaldata`) 中。

在 RStudio 中建立新的 RScript 檔案，並執行下列指令碼。 將 **ServerName** 取代為您自己的連線資訊。

```r
#Define the connection string to connect to the TutorialDB database
connStr <- "Driver=SQL Server;Server=ServerName;Database=TutorialDB;uid=Username;pwd=Password"


#Get the data from the table
library(RODBC)

ch <- odbcDriverConnect(connStr)

#Import the data from the table
rentaldata <- sqlFetch(ch, "dbo.rental_data")

#Take a look at the structure of the data and the top rows
head(rentaldata)
str(rentaldata)
```

您應該會看見如下所示的結果。

```results
   Year  Month  Day  RentalCount  WeekDay  Holiday  Snow
1  2014    1     20      445         2        1      0
2  2014    2     13       40         5        0      0
3  2013    3     10      456         1        0      0
4  2014    3     31       38         2        0      0
5  2014    4     24       23         5        0      0
6  2015    2     11       42         4        0      0
'data.frame':       453 obs. of  7 variables:
$ Year       : int  2014 2014 2013 2014 2014 2015 2013 2014 2013 2015 ...
$ Month      : num  1 2 3 3 4 2 4 3 4 3 ...
$ Day        : num  20 13 10 31 24 11 28 8 5 29 ...
$ RentalCount: num  445 40 456 38 23 42 310 240 22 360 ...
$ WeekDay    : num  2 5 1 2 5 4 1 7 6 1 ...
$ Holiday    : int  1 0 0 0 0 0 0 0 0 0 ...
$ Snow       : num  0 0 0 0 0 0 0 0 0 0 ...
```

## <a name="prepare-the-data"></a>準備資料

在此範例資料庫中，大部分的準備工作都已完成，但您在此將再執行一項準備。
使用下列 R 指令碼，藉由將資料類型變更為「因素」，將三個資料行識別為「類別」。



```r
#Changing the three factor columns to factor types
rentaldata$Holiday <- factor(rentaldata$Holiday);
rentaldata$Snow    <- factor(rentaldata$Snow);
rentaldata$WeekDay <- factor(rentaldata$WeekDay);



#Visualize the dataset after the change
str(rentaldata);
```

您應該會看見如下所示的結果。

```results
data.frame':      453 obs. of  7 variables:
$ Year       : int  2014 2014 2013 2014 2014 2015 2013 2014 2013 2015 ...
$ Month      : num  1 2 3 3 4 2 4 3 4 3 ...
$ Day        : num  20 13 10 31 24 11 28 8 5 29 ...
$ RentalCount: num  445 40 456 38 23 42 310 240 22 360 ...
$ WeekDay    : Factor w/ 7 levels "1","2","3","4",..: 2 5 1 2 5 4 1 7 6 1 ...
$ Holiday    : Factor w/ 2 levels "0","1": 2 1 1 1 1 1 1 1 1 1 ...
$ Snow       : Factor w/ 2 levels "0","1": 1 1 1 1 1 1 1 1 1 1 ...
```

資料現已備妥，可供訓練之用。

## <a name="clean-up-resources"></a>清除資源

如果您不打算繼續進行本教學課程，請刪除 TutorialDB 資料庫。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第二部分中，您學到了如何：

* 將範例資料載入 R 資料框架
* 藉由依某些資料行分類來以 R 準備資料

若要建立一個機器學習模型，使用 TutorialDB 資料庫中的資料，請遵循本教學課程系列的第三部分：

> [!div class="nextstepaction"]
> [使用 SQL 機器學習在 R 中建立預測模型](r-predictive-model-train.md)
