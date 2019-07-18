---
title: 使用 R-SQL Server 機器學習服務的資料庫內分析的教學課程
description: 了解如何內嵌 R 程式設計語言中 SQL Server 預存程序和 T-SQL 函式的程式碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8bf0485b63e341dbeff24a1974df840b0a28dfef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961896"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>教學課程：適用於 SQL 開發人員的 R 資料分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本教學課程中的 SQL 程式設計人員，透過建置和部署 R 為基礎的機器學習解決方案使用了解 R 整合[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)上 SQL Server 資料庫。 您將使用 T-SQL、 SQL Server Management Studio，並使用 [機器學習服務] 的資料庫引擎執行個體 ([Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)和 R 語言支援

本教學課程會向您介紹的資料模型化工作流程中使用的 R 函數。 步驟包括資料瀏覽、 建置及定型二元分類模型和部署模型。 您將建置此模型會預測一趟車程是否有可能導致提示，根據日期、 運動，距離和上車位置的時間。 

在本教學課程中使用的 R 程式碼的所有包裝在您建立和在 Management Studio 中執行的預存程序。

## <a name="background-for-sql-developers"></a>適用於 SQL 開發人員的背景

建置機器學習服務解決方案的程序很複雜，可包含多個工具和專家協調跨數個階段：

+ 取得和清除資料
+ 瀏覽資料及建置適用於模型化功能
+ 定型和微調模型
+ 部署至生產環境

實際的程式碼的開發和測試是最適合使用執行專用的 R 開發環境。 不過，指令碼經過完整測試之後，您可以輕鬆部署到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序在熟悉的環境中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

此多部分的教學課程的目的是移轉 「 完成 R 程式碼 」 至 SQL Server 的一般工作流程的簡介。 

- [第 1 課：瀏覽及視覺化資料圖形和散發，藉由預存程序呼叫 R 函數](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [第 2 課：在 T-SQL 函式中使用 R 建立資料特徵](sqldev-create-data-features-using-t-sql.md)
  
- [第 3 課：訓練及儲存使用函式和預存程序的 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [第 4 課：預測潛在的預存程序中使用 R 模型的結果](../tutorials/sqldev-operationalize-the-model.md)

模型儲存到資料庫之後，呼叫從預測模型[!INCLUDE[tsql](../../includes/tsql-md.md)]使用預存程序。

## <a name="prerequisites"></a>先決條件

所有的工作可使用[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

本教學課程假設您熟悉基本資料庫作業，例如建立資料庫和資料表、 匯入資料，以及撰寫 SQL 查詢。 它不會假設您知道。因此，提供所有 R 程式碼。 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation)或[SQL Server 2017 Machine Learning 服務以啟用 R](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [R 程式庫](../package-management/installed-package-information.md)

+ [Permissions](../security/user-permission.md)

+ [NYC 計程車示範資料庫](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [瀏覽及視覺化資料在預存程序中使用 R 函數](../tutorials/sqldev-explore-and-visualize-the-data.md)
