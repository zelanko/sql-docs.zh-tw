---
title: "什麼 &#39; s 機器學習服務的新功能 |Microsoft 文件"
ms.date: 01/08/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: "36"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: abbc7043f4eefe2c6f33a3f9fbc61fe0a97ceff9
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="whats-new-in-machine-learning-services-in-sql-server"></a>新功能 SQL Server 中的機器學習服務

在 SQL Server 2016 中，Microsoft 導入了 SQL Server R 服務，支援企業級資料科學，藉由整合 R 語言與 SQL Server 資料庫引擎的功能。

在 SQL Server 2017，資料庫整合的機器學習服務變得更強大了，加入對受歡迎的 Python 語言的支援。 對新語言的支援以及提供新名稱：**機器學習服務 （資料庫）**。

攔截最新的 announcement ！ [在 SQL Server 2017 Python： 增強式資料庫中的機器學習服務](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)

## <a name="whats-new-in-sql-server-2017"></a>SQL Server 2017 的新功能

SQL Server 中的機器學習伺服器提供用於建置及部署 Python 或 R 中的機器學習解決方案的完整支援。 以下是此版本的重點：

### <a name="whats-new-in-cumulative-update-3-for-sql-server-2017"></a>新功能 SQL Server 2017 累積更新 3

這個版本包含 Python 和 R 元件的更新。 

+ 已新增的支援 Python 模型中進行序列化 revoscalepy，使用 rx_serialize_model 函式

### <a name="in-database-python-integration"></a>資料庫 Python 整合

您可以在預存程序中執行 Python 或執行 Python 當成計算內容使用遠端 SQL Server 電腦。 這項整合會開啟新途徑 vast 的 Python 開發人員及資料科學家使用的 SQL Server 社群。

SQL Server 開發人員可以存取的更詳盡的 Python 程式庫的開放原始碼生態系統，包括熱門架構如 scikit-了解，TensorFlow、 Caffe 和 Theano/Keras。 並務必將這類創新瀏覽 microsoft **revoscalepy**和**microsoftml**！

資料庫中幾乎不執行 Python 機器學習的方式。 有很多其他潛在的應用程式整合與 SQL、 Python 和使用每種語言電源傳遞更智慧型、 功能強大的解決方案。

+ **revoscalepy**

    此版本包含的最終版本**revoscalepy**，其提供的 RevoScaleR 中的演算法的 Python 對等項目。 您可以建立線性和羅吉斯迴歸、 決策樹，促進式樹狀結構，以及隨機樹系中，所有可並行，並且可以在遠端計算內容中執行 Python 模型。

    如需詳細資訊，請參閱[何謂 revoscalepy](python/what-is-revoscalepy.md)。

+ Python 遠端計算內容

    此版本中支援多個資料來源和遠端計算內容使用。 資料科學家或開發人員可以執行遠端 SQL Server 上，瀏覽資料或建立模型，而不移動資料的 Python 程式碼。 使用遠端計算內容需要**revoscalepy**。

+ Python 支援在 Microsoft Machine Learning 伺服器 （獨立）

    [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)]包含安裝 Microsoft Machine Learning 伺服器的獨立版本的選項。 使用機器學習伺服器，您就可以發佈，並調整 R 或 Python 程式碼，而不需要使用 SQL Server。

### <a name="linux-support"></a>Linux 支援

使用 R 或 Python 資料庫內的機器學習服務目前不支援在 SQL Server on Linux。 尋找下一個版本的公告。

不過，在 Linux 上您可以執行[原生計分](sql-native-scoring.md)使用 T-SQL 的預測函數。 原生計分，可讓您從預先定型的模型非常快速，分數，而不需要呼叫，或甚至 R 執行階段。 這表示您可以使用 SQL Server on Linux 來產生預測的速度非常快，來服務用戶端應用程式。

### <a name="new-algorithms"></a>新的演算法

**MicrosoftML**的 R 和 Python 封裝包含的圖案狀態機器學習演算法和資料轉換可以縮放或執行中的遠端計算內容。 演算法包括可自訂的深度類神經網路、 快速的決策樹和決策樹、 線性迴歸和羅吉斯迴歸。 MicrosoftML 套件隨附 R 和 Python 的介面。

如需詳細資訊，請參閱[簡介 MicrosoftML](using-the-microsoftml-package.md)和[python microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)。

### <a name="operationalization"></a>實施

這個版本包含多個選項和功能，可協助您部署和散發機器學習工作：

+ 部署與整合使用 T-SQL 的機器 Python 解決方案

    Python 與 T-SQL 的整合意味著您可以呼叫任何 Python 程式碼使用`sp_execute_external_script`。 這個安全的基礎結構可讓企業級的 Python 模型和可從使用簡單的預存程序的應用程式呼叫的指令碼的部署。 從 SQL Python 程序及 MPI 環形平行處理的資料流資料是額外的效能。

+ **mrsdeploy** python

    **Mrsdeploy**封裝[!INCLUDE[rsql-platform-md](../includes/rsql-platformnew-md.md)]和[!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)]支援做為 web 服務的 Python 模型和指令碼部署。 如需其運作方式的範例，請參閱[發行和取用的 Python 程式碼](python/publish-consume-python-code.md)。

+ [效能]

    Microsoft 已推入的效能分數的界限。 使用中資料庫計分，我們會處理每百萬個資料列使用 R 模型的第二個。 在本版中的新功能**即時計分**和**原生計分**支援在單一資料列和批次計分的更佳的效能。

### <a name="realtime-scoring-and-native-scoring"></a>即時計分，和原生計分

即時計分會依賴原生 c + + 程式庫，以讀取以最佳化的二進位格式，儲存的模型，並不必呼叫 R 執行階段產生預測。 這可讓更快的計分作業。

此外，這一版的[!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)]包含快速計分，可以在任何版本的 SQL Server，即使在 Linux 上執行 「 原生的 T-SQL 函式。 此函式不需要安裝的 R 或額外的設定。 這表示您可以定型模型的其他位置，將它儲存在 SQL Server，然後再執行 計分而不需曾經呼叫。這項功能稱為_原生計分_。

  - 原生計分是僅適用於[!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)]。 它會使用在任何版本的 SQL Server，包括 Linux 可以執行的 T-SQL 函式。
 - 即時計分支援[!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)]，在 Microsoft Machine Learning 伺服器。 您可以執行預存程序，或執行即時計分的 R 程式碼。
 - 還有適用於 SQL Server 2016 中，如果執行個體升級為最新版的即時計分[!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]。

如需詳細資訊，請參閱下列文章：

 + [即時計分](real-time-scoring.md)
 + [原生評分](sql-native-scoring.md)
 + [如何執行即時計分或原生計分](r/how-to-do-realtime-scoring.md)

### <a name="upgrade-your-machine-learning-experience-and-get-pre-trained-models"></a>升級您的機器學習經驗並取得預先定型的模型

如果您已安裝舊版的 SQL Server 2016 R 服務，您可以立即升級為最新版本切換伺服器使用現代軟體生命週期原則。 如此一來，您可以利用 R 的更快的發行週期，並自動升級所有的 R 元件。 如需詳細資訊，請參閱[Server 機器學習中最新消息](https://docs.microsoft.com/machine-learning-server/whats-new-in-machine-learning-server)。

安裝程式也會提供安裝的預先定型的模型集合，以二進位格式的選項。 這些模型支援機器學習案例中，如影像辨識，其中，它可能很難尋找大型資料集來定型模型的客戶。 您安裝其中一個預先定型的模型之後，您可以預測使用您自己的資料，而不這類大型且複雜模型定型中所涉及的成本與時間。

如需詳細資訊，請參閱[安裝 SQL Server 中的 預先定型的模型](r/install-pretrained-models-sql-server.md)

### <a name="package-management"></a>封裝管理

這個版本包含許多增強功能中的 SQL Server 的封裝管理。 其中包括：

- 資料庫角色，以協助 DBA 管理封裝並指派權限才能安裝封裝
- 建立外部程式庫中的陳述式 T-SQL、 協助 Dba 管理封裝，而不需要知道 R
- 一組豐富的 R 函數，可協助安裝，請移除或列出使用者所擁有的封裝

如需詳細資訊，請參閱[封裝管理](r/r-package-management-for-sql-server-r-services.md)。

### <a name="get-started"></a>快速入門

+ [設定 SQL Server 機器學習服務中的 Python](../advanced-analytics/python/setup-python-machine-learning-services.md)

+ [設定 SQL Server 機器學習服務中的 R](r/set-up-sql-server-r-services-in-database.md)

+ [機器學習教學課程和範例](tutorials/machine-learning-services-tutorials.md)
