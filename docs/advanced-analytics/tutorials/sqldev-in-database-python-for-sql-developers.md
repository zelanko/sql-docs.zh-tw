---
title: 資料庫內 Python 分析適用於 SQL 開發人員 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 26703f73312b5531490afc7d01319d4ac290bebe
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2018
ms.locfileid: "49806758"
---
# <a name="in-database-python-analytics-for-sql-developers"></a>適用於 SQL 開發人員的資料庫內 Python 分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本逐步解說的目標是為 SQL 程式設計人員提供建置機器學習服務解決方案使用執行 SQL Server 中的 Python 的實際操作體驗。 在本逐步解說中，您將了解如何將 Python 程式碼加入至預存程序，並執行預存程序來建置，並從模型預測。

> [!NOTE]
> 偏好 R 嗎？ 請參閱[本教學課程](sqldev-in-database-r-for-sql-developers.md)，提供類似的解決方案，但使用 R，以及可以在 SQL Server 2016 或 SQL Server 2017 中執行。

## <a name="overview"></a>總覽

建置機器學習服務解決方案的程序很複雜，可包含多個工具和專家協調跨數個階段：

+ 取得和清除資料
+ 瀏覽資料及建置適用於模型化功能
+ 定型和微調模型
+ 部署至生產環境

**本逐步解說的焦點是建置和部署使用 SQL Server 的解決方案。**

資料是來自已知的紐約市計程車資料集。 若要讓這個逐步解說中，快速且輕鬆地，資料進行取樣。 您將建立二元分類模型來預測特定車程是否有可能獲得小費或不是，根據資料行，例如日、 距離和上車位置的時間。

所有的工作可使用[!INCLUDE[tsql](../../includes/tsql-md.md)]熟悉環境中的預存程序 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]


- [瀏覽及視覺化資料使用 Python](sqldev-py3-explore-and-visualize-the-data.md)

    執行基本的資料探索和視覺效果，從呼叫 python[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序。

- [在 T-SQL 中使用 Python 建立資料特徵](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    使用自訂 SQL 函數，建立新的資料特徵。
  
- [訓練及儲存使用 T-SQL Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    建置並儲存機器學習模型，在預存程序中使用 Python。
  
    本逐步解說示範如何執行二進位分類工作;您也可以使用資料建立用於迴歸或多級分類模型。

  
-  [ 實作 Python 模型](sqldev-py6-operationalize-the-model.md)

    模型儲存到資料庫之後，呼叫模型的預測使用[!INCLUDE[tsql](../../includes/tsql-md.md)]。

## <a name="requirements"></a>需求

### <a name="prerequisites"></a>先決條件

+ 使用 Machine Learning 服務與啟用的 Python 安裝 SQL Server 2017 執行的個體。 如需詳細資訊，請參閱 <<c0> [ 安裝 SQL Server 2017 Machine Learning 服務 （資料庫）](../install/sql-machine-learning-services-windows-install.md)。
+ 您用於本逐步解說的登入必須具有權限，可以建立資料庫和其他物件、上傳資料、選取資料，以及執行預存程序。

### <a name="experience-level"></a>經驗層級

您應該熟悉基本資料庫作業，例如建立資料庫和資料表、 資料匯入資料表，以及建立 SQL 查詢。

有經驗的 SQL 程式設計人員應該能夠在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，或執行所提供的 PowerShell 指令碼，來完成本逐步解說。

Python： 基本知識是很有用，但並非必要。 提供所有 Python 程式碼。

PowerShell 的一些知識會很有幫助。

### <a name="tools"></a>工具

本教學課程中，我們假設您已達到 「 部署 」 階段。 您有獲得清除資料、 完整的功能工程，以及使用 Python 程式碼的 T-SQL 程式碼。 因此，您可以完成本教學課程中使用 SQL Server Management Studio 或任何其他工具，可支援執行 SQL 陳述式。

+ [SQL Server 工具的概觀](https://docs.microsoft.com/sql/tools/overview-sql-tools) 

如果您想要開發及測試您自己的 Python 程式碼，或 Python 方案進行偵錯時，我們建議使用專用的開發環境：

+ **Visual Studio 2017**支援這兩個 R 並[Python](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/)。 我們建議[資料科學工作負載](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/)，其也支援 R 和 F #。
+ 如果您有舊版的 Visual Studio 中， [Visual Studio 的 Python 擴充功能](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio)輕鬆地管理多個 Python 環境。
+ PyCharm 是 Python 開發人員之間的熱門 IDE。

    > [!NOTE]
    > 一般情況下，避免撰寫或測試新的 Python 程式碼中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果您在預存程序中內嵌的程式碼有任何問題，從預存程序傳回的資訊通常不足以了解錯誤的原因。

若要協助您規劃及執行成功的機器學習服務專案中使用下列資源：

+ [Team Data Science Process](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview)

### <a name="estimated-time-required"></a>所需的預估的時間

|步驟| 時間 （小時）|
|----|----|
|下載範例資料| 0:15|
|使用 PowerShell 的 SQL server 匯入資料|0:15|
|瀏覽及視覺化資料|0:20|
|使用 T-SQL 建立資料特徵|0:30|
|訓練及儲存模型，使用 T-SQL|0:15|
|操作模型|0:40|

## <a name="get-started"></a>開始使用

  [步驟 1︰下載範例資料](demo-data-nyctaxi-in-sql.md)
