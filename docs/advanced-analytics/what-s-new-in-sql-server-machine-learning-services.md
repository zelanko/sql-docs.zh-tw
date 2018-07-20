---
title: 什麼&#39;的新功能 SQL Server 機器學習服務 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/02/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bf56d52823727609d713639d534e277be57caaef
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174805"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>什麼是 SQL Server Machine Learning 服務的新功能 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

機器學習服務功能會隨著我們持續展開、 擴充和強化的資料平台與資料科學，analytics 之間的整合至 SQL Server 加入每個版本中，並監督式的學習您想要實作您的資料。 

## <a name="new-in-sql-server-2017"></a>SQL Server 2017 的新功能

此版本新增 Python 支援和領先業界的機器學習服務演算法。 重新命名以反映新的範圍，SQL Server 2017 標示了**SQL Server Machine Learning 服務 （資料庫）**，使用 Python 和 r 語言支援 

此版也導入了**SQL Server Machine Learning Server （獨立式）**、 完全獨立的 SQL Server，針對您想要在專用的系統上執行的 R 和 Python 工作負載。 獨立伺服器，與您發佈及調整而不需使用 SQL Server 的 R 或 Python 的解決方案。

| 版本 | 功能更新 |
|---------|----------------|
| CU 6 | Bug 修正及套件重新整理，但沒有新功能公告。 修正包含 DateTime 資料類型的支援 SPEES 在查詢中為 Python 和改良的錯誤訊息，microsoftml 中預先定型的模型遺漏時。 |
| CU 5 | Bug 修正及套件重新整理，但沒有新功能公告。 修正會包含轉換函式和變數在 revoscalepy，更正長路徑中的相關錯誤 rxInstallPackages，修正在回送連線，RxExec rx_exec 函式，以及警告訊息的修訂中的增強功能。 |
| CU 4 | Bug 修正及套件重新整理，但沒有新功能公告。 |
| CU 3 | Python 模型序列化 revoscalepy，使用[rx_serialize_model 函式](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)。<br/><br/>[原生評分](sql-native-scoring.md)再加上的增強功能[即時評分](real-time-scoring.md)。 使用資料庫中評分，輸送量為每百萬個資料列使用 R 模型的第二個。 在此更新中，即時評分和原生評分提供較佳的效能，在單一資料列和批次評分。 原生評分使用 T-SQL 函式，以快速評分，可以執行 SQL Server，即使在 Linux 上的任何版本。 此函式不需要安裝的 R 或額外的設定。 這表示您可以訓練模型其他位置、 將它儲存在 SQL Server，然後再執行 評分，而不需要不斷呼叫。如需有關計分方法的詳細資訊，請參閱 <<c0> [ 如何執行即時計分或原生評分](r/how-to-do-realtime-scoring.md)。 |
| CU 2 | Bug 修正及套件重新整理，但沒有新功能公告。 |
| CU 1 | 在 revoscalepy，新增 從 SQL Server 資料來源，類似於傳回的結構描述資訊的 rx_create_col_info [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) for。 <br/><br/>增強[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)以支援平行處理的案例使用`RxLocalParallel`計算內容。|
| 最初發行 |[**在資料庫內分析 Python 整合**](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/) <br/><br/>[Revoscalepy](python/what-is-revoscalepy.md)封裝是 RevoScaleR 的 Python 對等。 您可以建立用於線性及羅吉斯迴歸、 決策樹、 梯度上升的樹和隨機樹系，所有可平行執行，且能夠在遠端計算內容中執行的 Python 模型。 此套件支援使用多個資料來源和遠端計算內容。 資料科學家或開發人員可以執行 Python 程式碼的遠端 SQL 伺服器上，瀏覽資料，或建立模型，而不移動資料。 <br/><br/>[Microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)封裝是相等的 Python MicrosoftML R 封裝。<br/><br/>透過 T-SQL 和 Python 整合[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。 您可以呼叫任何使用此預存程序的 Python 程式碼。 這個安全的基礎結構可讓企業級部署 Python 模型，您可以從使用簡單的預存程序的應用程式呼叫的指令碼。 從 SQL Python 程序和 MPI 通道平行處理的資料流處理資料，可達到進一步提高效能。 <br/><br/>您可以使用 T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md)函式來執行[原生評分](sql-native-scoring.md)上預先定型的模型，就已經先前儲存在所需的二進位格式。|
| 最初發行 | [**MicrosoftML (R)** ](using-the-microsoftml-package.md)包含的新狀態的機器學習服務演算法和資料可以縮放或執行中的遠端計算內容的轉換。 演算法會包括可自訂的深度類神經網路、 迅速的決策樹及決策樹、 線性迴歸和羅吉斯迴歸。 |
| 最初發行 | [**預先定型的模型**](install/sql-pretrained-models-install.md)影像辨識和正負面情感分析。 您可以使用這些模型來產生預測，根據您的資料。 |
| 最初發行 | [**R 套件管理**](r/install-additional-r-packages-on-sql-server.md)，包括下列重點： 資料庫角色來協助管理套件，並指派權限才能安裝封裝，DBA [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) T-SQL 陳述式協助 Dba 管理套件，而不需要知道 R、 和中的一組豐富的 R 函式[RevoScaleR](r/use-revoscaler-to-manage-r-packages.md)幫助您安裝、 移除或列出的封裝，使用者所擁有。 |
| 最初發行 | [**運算化，透過 mrsdeploy** ](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)部署和裝載為 web 服務的 R 指令碼。 適用於 R 指令碼只 （沒有 Python 對應項目）。 適用於 （獨立式） 的伺服器選項，以避免與其他 SQL Server 作業的資源競爭。 |


## <a name="new-in-sql-server-2016"></a>SQL Server 2016 的新功能

這個的版導入了機器學習服務透過 SQL server 的功能**SQL Server 2016 R Services**，處理 R 指令碼中的資料庫引擎執行個體的常駐資料的資料庫內分析引擎。

此外， **SQL Server 2016 R Server （獨立式）** 做為 Windows 伺服器上安裝 R Server 的方式發行。 一開始，SQL Server 安裝程式會提供唯一的方式，來安裝 R Server for Windows。 在更新版本中，開發人員和想要在 Windows 上的 R 伺服器的資料科學家可以使用另一個獨立安裝程式來達到相同的目標。 在 SQL Server 的獨立伺服器和獨立的伺服器產品的功能上相當[Microsoft R Server for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

| 版本 |功能更新 |
|---------|----------------|
| CU 的新增項目 | [**即時計分**](real-time-scoring.md)依賴原生 c + + 程式庫，以讀取最佳化的二進位格式，儲存在模型，則不必呼叫 R 執行階段產生預測。 這可讓評分作業更快。 使用即時評分，您可以執行預存程序，或執行即時計分的 R 程式碼。 即時評分也會提供適用於 SQL Server 2016 中，如果執行個體已升級至最新版本的[!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]。 |
| 最初發行 | [**R 的資料庫內分析整合**](r/sql-server-r-services.md)。 <br/><br/> 在 T-SQL，反之亦然，函式呼叫 R 的 R 套件。 RevoScaleR 函式提供大規模的 R 分析區塊資料處理成元件部分，協調和管理分散式處理和彙總結果。 在 SQL Server 2016 R Services （資料庫），與 database engine 執行個體，brining 資料和分析，一起在相同的處理內容中整合 RevoScaleR 引擎。 <br/><br/>透過 T-SQL 和 R 整合[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。 您可以呼叫任何使用此預存程序的 R 程式碼。 這個安全的基礎結構可讓企業級部署 Rn 模型和您可以從使用簡單的預存程序的應用程式呼叫的指令碼。 從 SQL R 處理序和 MPI 通道平行處理的資料流處理資料，可達到進一步提高效能。 <br/><br/>您可以使用 T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md)函式來執行[原生評分](sql-native-scoring.md)上預先定型的模型，就已經先前儲存在所需的二進位格式。|

## <a name="linux-support-roadmap"></a>Linux 支援藍圖

使用 R 或 Python 資料庫內的機器學習服務目前不支援在 Linux 上的 SQL Server。 尋找未來版本中的宣告。

不過，在 Linux 上您可以執行[原生評分](sql-native-scoring.md)使用 T-SQL 的預測函數。 原生評分，可讓您從預先定型的模型非常快速，而不需要呼叫，或甚至需要 R 執行階段進行評分。 這表示您可以在 Linux 上使用 SQL Server，來產生預測非常快速，以提供用戶端應用程式。

<a name="azure-sql-database-roadmap"></a>

## <a name="azure-sql-database-roadmap"></a>Azure SQL Database 的藍圖

沒有適用於 Azure SQL Database 中的 R 有限的支援： 僅適用於美國中部等美國，在進階層所建立的服務中。 展開的涵蓋範圍，包括 Python 支援，很可能在未來版本中遵循。 不過，這次沒有預訂的正式發行日期。  

## <a name="next-steps"></a>後續步驟

+ [安裝 SQL Server 2017 Machine Learning 服務 （資料庫）](install/sql-machine-learning-services-windows-install.md)
+ [機器學習服務教學課程和範例](tutorials/machine-learning-services-tutorials.md)
