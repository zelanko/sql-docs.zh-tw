---
title: 適用於 SQL Server 機器學習服務開發人員的內嵌的 R 分析教學課程 |Microsoft 文件
description: 教學課程顯示如何在 SQL Server 中內嵌 R 預存程序和 T-SQL 函數
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3d2b77d73bb1b8f5d4c507b884d0a09f4647012b
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2018
ms.locfileid: "35250021"
---
# <a name="tutorial-embedded-r-in-stored-procedures-and-t-sql-functions"></a>教學課程： 預存程序和 T-SQL 函式中內嵌 R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本教學課程的目標是提供 SQL 程式設計者建立的機器學習中 SQL Server 方案的實際操作體驗。 在此教學課程中，您將學習如何將 R 整合到應用程式或 BI 方案，方法是將 R 程式碼包裝在預存程序。

> [!NOTE]
> 
> Python 提供相同的方案。 需要 SQL Server 2017。 請參閱[資料庫內分析 Python 開發人員的](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>概觀

建立端對端解決方案的程序通常包含取得和清除資料、資料瀏覽和特徵工程、模型定型和微調，以及最後在生產環境中部署模型。 開發和測試的實際程式碼被執行使用專用的開發環境。 ，這可能表示 RStudio 或[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]。

不過，建立解決方案之後，您可以在熟悉的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境中，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 輕鬆地將它部署至 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

在此教學課程中，我們假設您有提供所需的方案，並專注於建置和部署使用 SQL Server 解決方案的 R 程式碼。

- [第 1 課： 下載的範例資料和指令碼](../tutorials/sqldev-download-the-sample-data.md)

- [第 2 課： 設定教學課程的環境](../r/sqldev-import-data-to-sql-server-using-powershell.md)

- [第 3 課： 瀏覽及視覺化資料圖形和散發，藉由呼叫預存程序中的 R 函數](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [第 4 課： 建立 T-SQL 函式中使用 R 資料功能](../tutorials/sqldev-create-data-features-using-t-sql.md)
  
- [第 5 課： 訓練並儲存使用函式和預存程序的 R 模型](../r/sqldev-train-and-save-a-model-using-t-sql.md)
  
- [第 6 課： 實施的預存程序中的包裝 R 程式碼](../tutorials/sqldev-operationalize-the-model.md)。 
  將模型儲存至資料庫之後，使用預存程序從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫要預測的模型。

## <a name="scenario"></a>狀況

本教學課程使用知名公用依據資料集，在 New York city taxis 往返。 若要讓範例程式碼執行更快速，我們會建立具代表性的 1%取樣的資料。 您將使用這項資料來建立二元分類模型來預測特定路線是否有可能取得提示，根據資料行，例如一天、 距離和收取位置的時間。

## <a name="requirements"></a>需求

本教學課程假設熟悉基本資料庫作業，例如建立資料庫和資料表、 匯入資料，以及撰寫 SQL 查詢。 它不會假設您知道。因此，提供所有的 R 程式碼。 技術的 SQL 程式設計人員可以使用提供的 PowerShell 指令碼，在 GitHub 上的範例資料和[!INCLUDE[tsql](../../includes/tsql-md.md)]中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]若要完成此範例。 

再開始本教學課程：

- 請確認您有設定的執行個體[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation)或[SQL Server 2017 機器學習服務以啟用 R](../install/sql-machine-learning-services-windows-install.md#verify-installation)。 此外，[確認您擁有的 R 程式庫](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)。
- 您使用此教學課程中的登入必須具有建立資料庫的權限和其他物件，若要上傳資料，選取 [資料]，然後執行預存程序。

> [!NOTE]
> 我們建議您執行**不**使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]撰寫或測試 R 程式碼。 如果您在預存程序中內嵌的程式碼有任何問題，從預存程序傳回的資訊是通常不足，無法了解錯誤的原因。
> 
> 偵錯時，我們建議您使用的工具，例如[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]，或 RStudio。 本教學課程中提供的 R 指令碼已使用傳統 R 工具進行部署及偵錯。

## <a name="next-lesson"></a>下一課

[第 1 課： 下載範例資料](../tutorials/sqldev-download-the-sample-data.md)
