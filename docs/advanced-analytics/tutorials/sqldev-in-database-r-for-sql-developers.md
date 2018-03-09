---
title: "資料庫內部 R 分析的 SQL 開發人員 （教學課程） |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: c18cb249-2146-41b7-8821-3a20c5d7a690
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 0062a75b92fc633e61b0aa73ae2c955ccd60cec5
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="in-database-r-analytics-for-sql-developers-tutorial"></a>資料庫內部 R 分析的 SQL 開發人員 （教學課程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本教學課程的目標是提供 SQL 程式設計者建立的機器學習中 SQL Server 方案的實際操作體驗。 在此教學課程中，您將學習如何將 R 整合到應用程式或 BI 方案，方法是將 R 程式碼包裝在預存程序。

> [!NOTE]
> 
> Python 提供相同的方案。 需要 SQL Server 2017。 請參閱[資料庫內分析 Python 開發人員的](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>概觀

建立端對端解決方案的程序通常包含取得和清除資料、資料瀏覽和特徵工程、模型定型和微調，以及最後在生產環境中部署模型。 開發和測試的實際程式碼被執行使用專用的開發環境。 ，這可能表示 RStudio 或[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]。

不過，建立解決方案之後，您可以在熟悉的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境中，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 輕鬆地將它部署至 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

在此教學課程中，我們假設您有提供所需的方案，並專注於建置和部署使用 SQL Server 解決方案的 R 程式碼。

- [第 1 課： 下載範例資料](../tutorials/sqldev-download-the-sample-data.md)

    將範例資料集和範例 SQL 指令碼檔下載至本機電腦。

- [第 2 課： 將資料匯入 SQL Server 使用 PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)

    執行 PowerShell 指令碼，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體上建立資料庫和資料表，並將範例資料載入資料表。

- [第 3 課： 探索和視覺化資料](../tutorials/sqldev-explore-and-visualize-the-data.md)

    從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序呼叫 R 套件和函數，以執行基本資料瀏覽和視覺效果。

- [第 4 課： 建立使用 T-SQL 資料功能](../tutorials/sqldev-create-data-features-using-t-sql.md)

    使用自訂 SQL 函數，建立新的資料特徵。
  
-   [第 5 課： 訓練並儲存使用 T-SQL R 模型](../r/sqldev-train-and-save-a-model-using-t-sql.md)

    建置在預存程序中使用 R 的機器學習模型。 將模型儲存至 SQL Server 資料表。
  
-   [第 6 課： 實施模型](../tutorials/sqldev-operationalize-the-model.md)

    將模型儲存至資料庫之後，使用預存程序從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫要預測的模型。

### <a name="scenario"></a>狀況

本教學課程使用知名公用依據資料集，在 New York city taxis 往返。 若要讓範例程式碼執行更快速，我們會建立具代表性的 1%取樣的資料。 您將使用這項資料來建立二元分類模型來預測特定路線是否有可能取得提示，根據資料行，例如一天、 距離和收取位置的時間。

### <a name="requirements"></a>需求

本教學課程適用於已熟悉基本資料庫作業，例如建立資料庫和資料表、 資料匯入資料表，以及建立 SQL 查詢的使用者。 其提供所有 R 程式碼，因此不需要 R 開發環境。 有經驗的 SQL 程式設計人員應該要能夠完成此範例使用[!INCLUDE[tsql](../../includes/tsql-md.md)]中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，以及執行所提供的 PowerShell 指令碼。

不過，再開始本教學課程，您必須完成下列準備工作：

- 連接到 SQL Server 2016 與 R Services 或 SQL Server 2017 機器學習服務與啟用 R 的執行個體。
- 您使用此教學課程中的登入必須具有建立資料庫的權限和其他物件，若要上傳資料，選取 [資料]，然後執行預存程序。

> [!NOTE]
> 我們建議您執行**不**使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]撰寫或測試 R 程式碼。 如果您在預存程序中內嵌的程式碼有任何問題，從預存程序傳回的資訊是通常不足，無法了解錯誤的原因。
> 
> 偵錯時，我們建議您使用的工具，例如[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]，或 RStudio。 本教學課程中提供的 R 指令碼已使用傳統 R 工具進行部署及偵錯。

## <a name="next-lesson"></a>下一課

[第 1 課： 下載範例資料](../tutorials/sqldev-download-the-sample-data.md)
