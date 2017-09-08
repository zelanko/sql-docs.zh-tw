---
title: "資料庫內 Python 分析的 SQL 開發人員 |Microsoft 文件"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 984ff8097b1f28cf11e28cc464c88dc3b9580a12
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="in-database-python-analytics-for-sql-developers"></a>資料庫內 Python 分析的 SQL 開發人員

本逐步解說的目標是為 SQL 程式設計者提供實際操作經驗，建立機器學習 SQL Server 中的方案。 在本逐步解說，您將學習如何將 Python 整合到應用程式中，將 Python 程式碼加入至預存程序。

> [!NOTE]
> 偏好 R 嗎？ 請參閱[本教學課程](sqldev-in-database-r-for-sql-developers.md)，這會提供類似的解決方案，但是會使用 R，並可以 eb 執行中 SQL Server 2016 或 SQL Server 2017。

## <a name="overview"></a>概觀

建立端對端解決方案的程序通常包含取得和清除資料、資料瀏覽和特徵工程、模型定型和微調，以及最後在生產環境中部署模型。 開發和測試的實際程式碼被執行比對使用專用的開發環境，例如這些的 Python 工具：

+ PyCharm，常用的 IDE
+ Spyder，隨附於[Visual Studio 2017](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/)如果您安裝[資料科學工作負載](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/)
+ [Visual Studio 的 Python 延伸](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio)。

您已建立，並在 IDE 中測試了方案之後，您可以部署 Python 程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序的熟悉環境[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

在本逐步解說中，我們假設您有獲得解決方案所需的 Python 程式碼，您將焦點放在建置和部署使用 SQL Server 方案。

- [步驟 1︰下載範例資料](sqldev-py1-download-the-sample-data.md)

  下載範例資料集和所有指令碼檔案到本機電腦上。

- [步驟 2︰使用 PowerShell 將資料匯入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

  執行指定的執行個體上建立資料庫和資料表，並載入到資料表的範例資料的 PowerShell 指令碼。

- [步驟 3：瀏覽及視覺化資料](sqldev-py3-explore-and-visualize-the-data.md)

  執行基本的資料探索和視覺效果，從呼叫 Python 由[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序。

- [步驟 4︰使用 T-SQL 建立資料特徵](sqldev-py5-train-and-save-a-model-using-t-sql.md)

  使用自訂 SQL 函數，建立新的資料特徵。
  
- [步驟 5︰使用 T-SQL 定型及儲存模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

   建置並儲存在預存程序中使用 Python 的機器學習模型。
  
-  [步驟 6︰操作模型](sqldev-py6-operationalize-the-model.md)

  模型儲存到資料庫之後，呼叫模型使用預測[!INCLUDE[tsql](../../includes/tsql-md.md)]。

> [!NOTE]
> 我們建議您不要使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]撰寫或測試的 Python 程式碼。 如果您在預存程序中內嵌的程式碼有任何問題，從預存程序傳回的資訊是通常不足，無法了解錯誤的原因。


### <a name="scenario"></a>狀況

本逐步解說使用已知的紐約市計程車資料集。 若要讓這個逐步解說中，快速且輕鬆，取樣資料。 使用這項資料，您將建立二元分類模型來預測特定路線是否有可能取得提示，根據資料行，例如一天、 距離和收取位置的時間。

### <a name="requirements"></a>需求

本逐步解說適用於已熟悉基本資料庫作業的使用者，這些作業包括建立資料庫和資料表、將資料匯入資料表，以及建立 SQL 查詢等等。

提供所有的 Python 程式碼。 有經驗的 SQL 程式設計人員應該能夠在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，或執行所提供的 PowerShell 指令碼，來完成本逐步解說。

再開始逐步解說，您必須完成下列準備工作：

- 機器學習服務與啟用的 Python 安裝執行個體的 SQL Server 2017 （需要 CTP 2.0 或更新版本）。
- 您用於本逐步解說的登入必須具有權限，可以建立資料庫和其他物件、上傳資料、選取資料，以及執行預存程序。

## <a name="next-step"></a>下一個步驟

  [步驟 1︰下載範例資料](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>另請參閱

[使用 Python 的機器學習服務](../python/sql-server-python-services.md)



