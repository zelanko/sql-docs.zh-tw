---
title: "什麼&#39;的新功能 SQL Server 機器學習服務 |Microsoft 文件"
ms.date: 03/08/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 4a3b7c8c389d471abe932faea64b44a14ac034ab
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2018
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>新功能 SQL Server 機器學習服務 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

機器學習功能會加入至 SQL Server 中每個發行我們繼續依序展開、 擴充和加深資料平台與資料科學，分析，之間的整合，和監督式的學習您想要實作您的資料。 

## <a name="new-in-sql-server-2017"></a>SQL Server 2017 的新功能

此版本新增 Python 支援業界領先的機器學習演算法。 重新命名以反映新的範圍，SQL Server 2017 引進的 SQL Server 機器學習服務 （資料庫），以標示 Python 和 r 語言支援 

此版本也導入了 SQL Server 機器學習伺服器 （獨立），完全獨立的 SQL Server R，並將 Python 您想要在專用的系統上執行的工作負載。 與獨立伺服器，您可以發佈並調整 R 或 Python 程式碼，而不需要使用 SQL Server。

| 版本 | 功能更新 |
|---------|---------------|
| CU 4 | Bug 修正和封裝重新整理，但不是新增功能的公告。 |
| CU 3 | 1.Python 模型 revoscalepy 中的序列化使用[rx_serialize_model 函式](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)。<br/><br/>2.[原生計分](sql-native-scoring.md)再加上的增強功能[即時計分](real-time-scoring.md)。 使用中資料庫計分，輸送量為每百萬個資料列使用 R 模型的第二個。 在此更新中，即時計分，和原生計分提供更佳的效能，在單一資料列和批次計分。 計分會使用原生快速計分的 T-SQL 函式可以執行的 SQL Server，即使在 Linux 上的任何版本。 此函式不需要安裝的 R 或額外的設定。 這表示您可以定型模型的其他位置，將它儲存在 SQL Server，然後再執行 計分而不需曾經呼叫。如需有關計分方法的詳細資訊，請參閱[如何執行即時計分或原生計分](r/how-to-do-realtime-scoring.md)。 |
| CU 2 | Bug 修正和封裝重新整理，但不是新增功能的公告。 |
| CU 1 | 1.在 revoscalepy，會加入傳回結構描述資訊從 SQL Server 資料來源，類似於 rx_create_col_info [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo)如。 <br/><br/>2.若要增強功能[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)支援平行案例使用`RxLocalParallel`計算內容。|
| 最初發行 |[**分析資料庫中的 Python 支援**](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/) <br/><br/>[Revoscalepy](python/what-is-revoscalepy.md)封裝是 RevoScaleR Python 等同於。 您可以建立線性和羅吉斯迴歸、 決策樹，促進式樹狀結構，以及隨機樹系中，所有可並行，並且可以在遠端計算內容中執行 Python 模型。 此套件支援使用多個資料來源和遠端計算內容。 資料科學家或開發人員可以執行遠端 SQL Server 上，瀏覽資料或建立模型，而不移動資料的 Python 程式碼。 <br/><br/>[Microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)封裝是 MicrosoftML R 封裝的 Python 對等。<br/><br/>透過 T-SQL 和 Python 整合[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。 您可以呼叫任何使用此預存程序的 Python 程式碼。 這個安全的基礎結構可讓企業級的 Python 模型和可從使用簡單的預存程序的應用程式呼叫的指令碼的部署。 額外的效能提升可達到資料流資料從 SQL Python 程序及 MPI 環形平行化作業。 |
| 最初發行 | [**MicrosoftML (R)** ](using-the-microsoftml-package.md)包含的圖案狀態機器學習演算法和資料轉換可以縮放或執行中的遠端計算內容。 演算法包括可自訂的深度類神經網路、 快速的決策樹和決策樹、 線性迴歸和羅吉斯迴歸。 |
| 最初發行 | [**預先定型的模型**](r/install-pretrained-models-sql-server.md)影像辨識和正負數情緒分析。 您可以使用這些模型來產生您自己的資料上的預測。 |
| 最初發行 | [**封裝管理**](r/r-package-management-for-sql-server-r-services.md)，包括下列重點： 資料庫角色來協助管理封裝並指派權限才能安裝封裝，DBA[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)中 T-SQL 陳述式說明 Dba 管理封裝，而不需要知道 R，和一組豐富的 R 函數中[RevoScaleR](r/use-revoscaler-to-manage-r-packages.md)協助安裝、 移除或列出封裝，使用者所擁有。 |
| 最初發行 | [**透過 mrsdeploy 實施**](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)用於部署和裝載為 web 服務的 R 指令碼。 適用於 R 指令碼只 （沒有 Python 對等）。 適用於 [（獨立） 伺服器] 選項，以避免與其他 SQL Server 作業的資源競爭。 |


## <a name="new-in-sql-server-2016"></a>SQL Server 2016 的新功能

學習功能到 SQL Server 透過此版導入了機器**SQL Server 2016 R Services**，資料庫中分析引擎常駐的資料庫引擎執行個體資料處理 R 指令碼。

此外， **SQL Server 2016 R 伺服器 （獨立）**做為 Windows server 上安裝 R Server 的方式發行。 一開始，SQL Server 安裝程式會提供安裝 R Server for Windows 的唯一方式。 在更新版本中，開發人員和想要在 Windows 上的 R 伺服器的資料科學家可以使用另一個獨立安裝程式來達到相同的目標。 SQL Server 中的獨立伺服器功能上相當於獨立的伺服器產品[Microsoft R Server for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

| 版本 |功能更新 |
|---------|----------------|
| CU | [即時計分](real-time-scoring.md)。 即時計分會依賴原生 c + + 程式庫，以讀取以最佳化的二進位格式，儲存的模型，並不必呼叫 R 執行階段產生預測。 這可讓更快的計分作業。 使用即時計分，您可以執行預存程序，或執行即時計分的 R 程式碼。 還有適用於 SQL Server 2016 中，如果執行個體升級為最新版的即時計分[!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]。 |
| 最初發行 | R 封裝和解譯器呼叫函式在 T-SQL，反之亦然。<br/>RevoScaleR 函數提供大規模的 R 分析區塊資料處理成元件部分，協調和管理分散式處理和彙總結果。 SQL Server 2016 R 服務 （資料庫），RevoScaleR 引擎整合資料庫引擎執行個體，brining 資料與分析一起放在相同的處理內容。 |

## <a name="linux-support-roadmap"></a>Linux 支援藍圖

使用 R 或 Python 資料庫內的機器學習服務目前不支援在 SQL Server on Linux。 尋找下一個版本的公告。

不過，在 Linux 上您可以執行[原生計分](sql-native-scoring.md)使用 T-SQL 的預測函數。 原生計分，可讓您從預先定型的模型非常快速，分數，而不需要呼叫，或甚至 R 執行階段。 這表示您可以使用 SQL Server on Linux 來產生預測的速度非常快，來服務用戶端應用程式。

### <a name="next-steps"></a>後續的步驟

+ [安裝 SQL Server 機器學習服務](../advanced-analytics/python/setup-python-machine-learning-services.md)
+ [機器學習教學課程和範例](tutorials/machine-learning-services-tutorials.md)
