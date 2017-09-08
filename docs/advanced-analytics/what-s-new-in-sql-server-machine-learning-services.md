---
title: "什麼 & #39 的新機器學習服務 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8719ec8be1c0f7b7b0dc72093707829c30ebbb3f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="whats-new-in-machine-learning-services-in-sql-server"></a>新功能 SQL Server 中的機器學習服務

在 SQL Server 2016 中，Microsoft 導入了 SQL Server R 服務，支援企業級資料科學，藉由整合 R 語言與 SQL Server 資料庫引擎的功能。

SQL Server 2017，在機器學習變得更強大了，加入對受歡迎的 Python 語言的支援。 對新語言的支援以及提供新名稱：**機器學習服務 （資料庫）**。

攔截最新的 announcement ！ [在 SQL Server 2017 Python： 增強式資料庫中的機器學習服務](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)

## <a name="whats-new-in-sql-server-2017-release-candidate-2"></a>SQL Server 2017 候選版 2 中最新消息

Microsoft 機器學習 Server SQL Server 中現在會提供用於建置及部署機器學習解決方案的完整支援。 以下是此版本的重點：

> [!IMPORTANT]
> 
> 機器學習服務，包括使用 R 或 Python，目前不支援執行 SQL Server on Linux，或 Azure SQL 資料庫中時。 尋找下一個版本的變更。
> 
> 不過，原生計分使用預測函數是目前支援的 Linux 版本。 
 
### <a name="in-database-python-integration"></a>資料庫 Python 整合

您可以在預存程序中執行 Python 或執行 Python 當成計算內容使用遠端 SQL Server 電腦。 這項整合會開啟新的 Python 開發人員及資料科學家使用的 SQL Server，以及以例如，microsoft 瀏覽創新 vast 社群途徑**revoscalepy**和**microsoftml**.

SQL Server 開發人員可以存取的更詳盡的 Python 程式庫的開放原始碼生態系統，包括熱門架構如 scikit-了解，Tensorflow、 Caffe 和 Theano/Keras。 

但執行的 Python 資料庫中不是只為機器學習服務;有各種整合 Python SQL，利用個別的語言，以提供更智慧型、 功能強大的解決方案的優點與其他潛在的應用程式。

+ **revoscalepy**

    此版本包含的最終版本**revoscalepy**，其中提供資料流中 RevoScaleR 演算法的可擴充 Pythonic 對等項目。 您可以建立線性和羅吉斯迴歸、 決策樹，促進式樹狀結構，以及隨機樹系中，所有可並行，並且可以在遠端計算內容中執行 Python 模型。

    如需詳細資訊，請參閱[何謂 revoscalepy](python/what-is-revoscalepy.md)。

+ Python 遠端計算內容

    此版本中支援多個資料來源和遠端計算內容使用。 資料科學家或開發人員可以執行遠端 SQL Server 上，瀏覽資料或建立模型，而不移動資料的 Python 程式碼。 使用遠端計算內容需要**revoscalepy**。

+ Python 支援在 Microsoft Machine Learning 伺服器 （獨立）

    SQL Server 2017 包括安裝 Python 和 R 的平台的獨立版本的選項。 使用機器學習伺服器，您就可以發佈，並調整 R 或 Python 程式碼，而不需要使用 SQL Server。

    在 Microsoft Machine Learning 伺服器 Python 用途的範例，請參閱[發行和取用的 Python 程式碼](python/publish-consume-python-code.md)。

### <a name="new-algorithms"></a>新的演算法

**MicrosoftML**的 R 和 Python 封裝包含的圖案狀態機器學習演算法和資料轉換可以縮放或執行中的遠端計算內容。 演算法包括可自訂的深度類神經網路、 快速的決策樹和決策樹、 線性迴歸和羅吉斯迴歸。

MicrosoftML 套件會隨附 R 和 Python 介面，而且 Microsoft 機器學習 Server 9.2.0 版本為基礎。

如需詳細資訊，請參閱[簡介 MicrosoftML](using-the-microsoftml-package.md)和[python microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)。

### <a name="operationalization"></a>實施

這個版本包含多個選項和功能，可協助您部署和散發機器學習工作：

+ 利用 T-SQL 實施

    Python 與 T-SQL 的整合意味著您可以呼叫任何 Python 程式碼使用`sp_execute_external_script`。 這個安全的基礎結構可讓企業級的 Python 模型和可從使用簡單的預存程序的應用程式呼叫的指令碼的部署。 從 SQL Python 程序及 MPI 環形平行處理的資料流資料是額外的效能。

+ **mrsdeploy** python

    **Mrsdeploy**封裝的 Microsoft R Server 現在支援為 web 服務的 Python 模型和指令碼部署，且可在機器學習伺服器 （獨立） 的選項。 如需其運作方式的範例，請參閱[發行和取用的 Python 程式碼](python/publish-consume-python-code.md)。

+ 效能

    Microsoft 已推入的效能分數的界限。 使用中資料庫計分，我們會處理每百萬個資料列使用 R 模型的第二個。 在本版中的新功能**即時計分**和**原生計分**支援單一資料列評分和小型較佳的效能以及批次。 

### <a name="realtime-scoring-and-native-scoring"></a>即時計分，和原生計分

即時計分會依賴原生 c + + 程式庫，以讀取以最佳化的二進位格式，儲存的模型，並不必呼叫 R 執行階段產生預測。 這可讓更快的計分作業。

此外，這一版的 SQL Server 2017 包含原生 T-SQL 函式的快速計分可在任何版本的 SQL Server，即使在 Linux 上執行。 此函式不需要安裝的 R 或額外的設定。 這表示您可以定型模型的其他位置，將它儲存在 SQL Server，然後再執行 計分而不需曾經呼叫。這項功能稱為_原生計分_。

  - 原生計分是僅適用於 SQL Server 2017。 它會使用在任何版本的 SQL Server，包括 Linux 可以執行的 T-SQL 函式。
 - 在 SQL Server 2017，和 Microsoft Machine Learning 伺服器都支援即時計分。 您可以 runa 預存程序或執行即時計分的 R 程式碼。
 - 適用於 SQL Server 2016 中，如果執行個體升級為最新版的 Microsoft R Server 也是即時計分。

如需詳細資訊，請參閱下列文章：

 + [即時計分](real-time-scoring.md)
 + [原生計分](sql-native-scoring.md)
 + [如何執行即時計分或原生計分](r/how-to-do-realtime-scoring.md)

### <a name="upgrade-your-ml-experience-and-get-pre-trained-models"></a>升級您的 ML 經驗並取得預先定型的模型

如果您已安裝舊版的 SQL Server 2016 R 服務，您可以立即升級為最新版本切換伺服器使用現代的生命週期原則。 如此一來，您可以利用 R 的更快的發行週期，並自動升級所有的 R 元件。 如需詳細資訊，請參閱 [Microsoft R Server 9.0.1 (英文)](https://docs.microsoft.com/r-server/whats-new-in-r-server)。

安裝程式也會提供安裝的預先定型的模型集合，以二進位格式的選項。 這些模型支援機器學習案例中，如影像辨識，其中，它可能很難尋找大型資料集來定型模型的客戶。 您安裝其中一個預先定型的模型之後，您可以預測使用您自己的資料，而不這類大型且複雜模型定型中所涉及的成本與時間。

如需詳細資訊，請參閱[安裝 SQL Server 中的 預先定型的模型](r/install-pretrained-models-sql-server.md)

### <a name="package-management"></a>封裝管理

這個版本包含許多增強功能中的 SQL Server 的封裝管理。 其中包括：

- 資料庫角色，以協助 DBA 管理和稽核權限
- 建立 EXTERAL 文件庫中的陳述式 T-SQL
- 一組豐富的 R 函數，可協助安裝，請移除或列出使用者所擁有的封裝。

如需詳細資訊，請參閱[封裝管理](r/r-package-management-for-sql-server-r-services.md)。

### <a name="get-started"></a>快速入門

+ [設定 SQL Server 機器學習服務中的 Python](../advanced-analytics/python/setup-python-machine-learning-services.md)

+ [設定 SQL Server 機器學習服務中的 R](r/set-up-sql-server-r-services-in-database.md)

+ [機器學習教學課程](tutorials/machine-learning-services-tutorials.md)
