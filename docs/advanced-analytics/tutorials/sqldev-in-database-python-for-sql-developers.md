---
title: "資料庫內 Python 分析的 SQL 開發人員 |Microsoft 文件"
ms.custom: 
ms.date: 10/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 1f6a1279268668062c83a151b6e7235b5c873325
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="in-database-python-analytics-for-sql-developers"></a>在資料庫 Python 分析的 SQL 開發人員

本逐步解說的目標是提供 SQL 程式設計者建立的機器學習解決方案使用 SQL Server 中執行的 Python 的實際操作體驗。 在本逐步解說，您將學習如何將 Python 程式碼加入至預存程序，並執行預存程序來建置，並預測模型。

> [!NOTE]
> 偏好 R 嗎？ 請參閱[本教學課程](sqldev-in-database-r-for-sql-developers.md)，前者可以提供類似的解決方案，但會使用 R，並可以在執行 SQL Server 2016 或 SQL Server 2017。

## <a name="overview"></a>概觀

建立機器學習解決方案的程序很複雜，可包含多個工具和相關主題專家協調跨數個階段：

+ 取得及清除資料
+ 瀏覽資料及建置模型很有用的功能
+ 定型集和微調模型
+ 部署至生產環境

**本逐步解說的重點是在建置和部署使用 SQL Server 的方案。**

資料是來自已知 NYC 計程車資料集。 若要讓這個逐步解說中，快速且輕鬆，取樣資料。 您將建立二元分類模型來預測特定路線是否有可能取得提示，根據資料行，例如一天、 距離和收取位置的時間。

所有工作，都才可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)]熟悉環境中的預存程序[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]

- [步驟 1︰下載範例資料](sqldev-py1-download-the-sample-data.md)

    下載範例資料集和所有指令碼檔案到本機電腦上。

- [步驟 2︰使用 PowerShell 將資料匯入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

    執行指定的執行個體上建立資料庫和資料表，並載入到資料表的範例資料的 PowerShell 指令碼。

- [步驟 3： 探索和視覺化的資料，使用 Python](sqldev-py3-explore-and-visualize-the-data.md)

    執行基本的資料探索和視覺效果，從呼叫 Python 由[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序。

- [步驟 4： 建立使用 Python T-SQL 中的資料功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    使用自訂 SQL 函數，建立新的資料特徵。
  
- [步驟 5： 訓練並儲存使用 T-SQL Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    建置並儲存在預存程序中使用 Python 的機器學習模型。
  
    本逐步解說示範如何執行成二元分類工作。您也可以使用資料來建立用於迴歸或多級分類模型。

  
-  [步驟 6： 實施 Python 模型](sqldev-py6-operationalize-the-model.md)

    模型儲存到資料庫之後，呼叫模型使用預測[!INCLUDE[tsql](../../includes/tsql-md.md)]。

## <a name="requirements"></a>需求

### <a name="prerequisites"></a>必要條件

+ 機器學習服務與啟用的 Python 安裝 SQL Server 2017 的執行個體。 如需詳細資訊，請參閱[設定 SQL Server 機器學習服務使用 Python](../python/setup-python-machine-learning-services.md)。
+ 您用於本逐步解說的登入必須具有權限，可以建立資料庫和其他物件、上傳資料、選取資料，以及執行預存程序。

### <a name="experience-level"></a>遇到層級

您應該熟悉基本資料庫作業，例如建立資料庫和資料表、 資料匯入資料表，以及建立 SQL 查詢。

有經驗的 SQL 程式設計人員應該能夠在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，或執行所提供的 PowerShell 指令碼，來完成本逐步解說。

Python： 基本知識是很有用，但並非必要。 提供所有的 Python 程式碼。

PowerShell 的一些知識會很有幫助。

### <a name="tools"></a>工具

此教學課程中，我們假設您已達到部署階段。 您已獲得清理資料，請完成功能工程，及使用 Python 程式碼的 T-SQL 程式碼。 因此，您可以完成本教學課程中使用 SQL Server Management Studio 或任何其他工具，可支援執行 SQL 陳述式。

+ [SQL Server 工具的概觀](https://docs.microsoft.com/sql/tools/overview-sql-tools) 

如果您想要開發並測試您的 Python 程式碼，或 Python 方案進行偵錯時，建議使用專用的開發環境：

+ **Visual Studio 2017**支援這兩個 R 和[Python](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/)。 我們建議[資料科學工作負載](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/)，其也支援 R 和 F #。
+ 如果您有舊版的 Visual Studio 中， [for Visual Studio 的 Python 延伸](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio)輕鬆地管理多個 Python 環境。
+ PyCharm 是 Python 開發人員之間的熱門 IDE。

    > [!NOTE]
    > 一般情況下，應避免撰寫，或是測試新的 Python 程式碼中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果您在預存程序中內嵌的程式碼有任何問題，從預存程序傳回的資訊是通常不足，無法了解錯誤的原因。

使用下列資源可協助您規劃及執行成功的機器學習服務專案：

+ [資料科學的小組流程](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview)

### <a name="estimated-time-required"></a>所需的預估的時間

|步驟| 時間 （小時）|
|----|----|
|下載範例資料| 0:15|
|若要使用 PowerShell 的 SQL Server 匯入資料|0:15|
|探索和視覺化資料|0:20|
|建立使用 T-SQL 資料功能|0:30|
|訓練和儲存模型，使用 T-SQL|0:15|
|實施模型|0:40|

## <a name="get-started"></a>快速入門

  [步驟 1︰下載範例資料](sqldev-py1-download-the-sample-data.md)
