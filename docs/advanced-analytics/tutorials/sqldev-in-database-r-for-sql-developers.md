---
title: 使用 R 和 SQL Server 機器學習服務的資料庫內分析的教學課程 |Microsoft Docs
description: 教學課程示範如何在 SQL Server 中內嵌 R 預存程序和 T-SQL 函數
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8c7296c46bb6312d66c07c0bb63c9e97c37ec1db
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082430"
---
# <a name="tutorial-learn-in-database-analytics-using-r-in-sql-server"></a>教學課程： 了解在 SQL Server 中使用 R 的資料庫內分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本教學課程適用於 SQL 程式設計人員，您可以使用 R 語言來建置和部署機器學習解決方案的 R 程式碼包裝在預存程序的實際操作體驗。

本教學課程會使用已知公用資料集，根據紐約市計程車車程。 若要讓範例程式碼執行更快速，我們建立具代表性的 1%取樣資料。 您將使用此資料建置二元分類模型來預測特定車程是否有可能獲得小費或不是，根據資料行，例如日、 距離和上車位置的時間。

> [!NOTE]
> 
> 在 Python 中使用相同的方案。 需要 SQL Server 2017。 請參閱[資料庫內分析適用於 Python 開發人員](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>概觀

通常建置端對端解決方案的程序包含取得和清除資料、 資料探索和特徵工程、 模型定型和微調，和最後在生產環境中將模型部署。 實際的程式碼的開發和測試是最適合執行使用專用的開發環境。 針對 R，這可能表示 RStudio 或[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]。

不過，建立解決方案之後，您可以在熟悉的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境中，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 輕鬆地將它部署至 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

- [第 1 課︰ 下載範例資料和指令碼](../tutorials/sqldev-download-the-sample-data.md)

- [第 2 課： 設定教學課程的環境](../r/sqldev-import-data-to-sql-server-using-powershell.md)

- [第 3 課： 探索和視覺化 預存程序呼叫 R 函式的 資料圖形和散發](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [第 4 課： 建立在 T-SQL 函式中使用 R 的資料特徵](../tutorials/sqldev-create-data-features-using-t-sql.md)
  
- [第 5 課： 訓練及儲存使用函式和預存程序的 R 模型](../r/sqldev-train-and-save-a-model-using-t-sql.md)
  
- [第 6 課： 運算化的預存程序中的換行 R 程式碼](../tutorials/sqldev-operationalize-the-model.md)。 
  將模型儲存至資料庫之後，使用預存程序從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫要預測的模型。

## <a name="prerequisites"></a>先決條件

本教學課程假設您熟悉基本資料庫作業，例如建立資料庫和資料表、 匯入資料，以及撰寫 SQL 查詢。 它不會假設您知道。因此，提供所有 R 程式碼。 技術熟練的 SQL 程式設計人員可以使用提供的 PowerShell 指令碼，在 GitHub 上的範例資料並[!INCLUDE[tsql](../../includes/tsql-md.md)]在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]若要完成此範例。 

再開始本教學課程：

- 請確認您有設定的執行個體[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation)或是[SQL Server 2017 Machine Learning 服務以啟用 R](../install/sql-machine-learning-services-windows-install.md#verify-installation)。 此外，[確認您可以使用 R 程式庫](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)。
- 您用於本教學課程中的登入必須擁有建立資料庫的權限和其他物件，來上傳資料，選取 [資料]，並執行預存程序。

> [!NOTE]
> 我們建議您不要**未**使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]撰寫或測試 R 程式碼。 如果您在預存程序中內嵌的程式碼有任何問題，從預存程序傳回的資訊通常不足以了解錯誤的原因。
> 
> 我們建議您進行偵錯，您使用的工具，例如[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]，或 RStudio。 本教學課程中提供的 R 指令碼已使用傳統 R 工具進行部署及偵錯。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [第 1 課︰ 下載範例資料](../tutorials/sqldev-download-the-sample-data.md)