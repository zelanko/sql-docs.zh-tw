---
title: SQL Server 機器學習服務的新功能
titleSuffix: ''
description: 適用於 SQL Server 機器學習服務和 SQL Server 2016 R Services 每個版本的新功能公告。
ms.date: 11/17/2020
ms.topic: overview
author: dphansen
ms.author: davidph
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning-services
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8d0da76c639048e9479afd575b584275a9bb51c6
ms.sourcegitcommit: d2dba862814c60f00b16d4e412bf673b2c0dee5f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94810508"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>SQL Server 機器學習服務的新功能
[!INCLUDE [SQL Server 2016 and later](../includes/applies-to-version/sqlserver2016.md)]

本文說明每個 [SQL Server 機器學習服務](sql-server-machine-learning-services.md)版本中所包含的新功能。 在我們繼續擴充、延伸並加深資料平台、進階分析及資料科學之間的整合時，便會將機器學習功能新增至每個版本的 SQL Server 中。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019"></a>SQL Server 2019 的新功能

此版本會在 SQL Server 中新增適用於 Python 和 R 機器學習作業的熱門要求功能。 如需此版本中所有功能的詳細資訊，請參閱 [SQL Server 2019 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)與 [SQL Server 2019 的版本資訊](../sql-server/sql-server-version-15-release-notes.md)。

> [!NOTE]
> 如需 SQL Server 2019 中關於 Java 的新功能文件，請參閱 [SQL Server 語言擴充功能中有哪些新功能？](../language-extensions/language-extensions-whats-new.md) \(英文\)

以下是 SQL Server 機器學習服務的新功能，可在 **Windows** 及 **Linux** 上使用：

- 已在適用於 Python 和 R 的機器學習服務中新增 Linux 平台支援。從 [在 Linux 上安裝 SQL Server 機器學習服務](../linux/sql-server-linux-setup-machine-learning.md) 開始使用。
- [從 Python 或 R 指令碼對 SQL Server 的回送連線](connect/loopback-connection.md)。 
- [建立適用於 Python 及 R 的外部程式庫 (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md)。
- [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) \(部分機器翻譯\) 引進兩個新的參數，可讓您從分割的資料輕鬆產生多個模型。 若要深入了解，請參閱此教學課程：[在 R 中建立資料分割型模型](tutorials/r-tutorial-create-models-per-partition.md)。
- Launchpad 服務已可使用容錯移轉叢集支援，前提是已在所有節點上啟動 SQL Server Launchpad 服務。 如需詳細資訊，請參閱 [SQL Server 容錯移轉叢集安裝](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)。
- 機器學習服務的隔離機制變更。 如需詳細資訊，請參閱 [Windows 上的 SQL Server 2019：機器學習服務的隔離變更](install/sql-server-machine-learning-services-2019.md)

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>SQL Server 2017 的新功能

此版本新增 [Python 支援和領先業界的機器學習演算法](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/) \(英文\)。 SQL Server 2017 引進為了反映新範圍而重新命名的 [SQL Server 機器學習服務 (資料庫內)](sql-server-machine-learning-services.md)，並針對 Python 和 R 提供語言支援。 

如需完整的功能公告，請參閱 [SQL Server 2017 的新功能](../sql-server/what-s-new-in-sql-server-2017.md)。

### <a name="r-enhancements"></a>R 增強功能

SQL Server 機器學習服務的 R 元件是新一代的 SQL Server 2016 R Services，並具有更新版本的基底 R、RevoScaler 及其他套件。

R 的新功能包括 [**套件管理**](package-management/install-r-packages-with-tsql.md)，並具有下列重點： 

+ 資料庫角色可協助 DBA 針對套件安裝管理套件及指派權限。
+ [CREATE EXTERNAL LIBRARY](../t-sql/statements/create-external-library-transact-sql.md) 能協助 DBA 以熟悉的 T-SQL 語言來管理套件。
+ [RevoScaleR](package-management/install-r-packages-with-revoscaler.md) 函數可協助安裝、移除或列出使用者所擁有的套件。 如需詳細資訊，請參閱[如何使用 RevoScaleR 函數在 SQL Server 上尋找或安裝 R 套件](package-management/install-r-packages-with-revoscaler.md)。

### <a name="r-libraries"></a>R 程式庫

| Package | 描述 |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | 在此版本中，MicrosoftML 會包含在預設的 R 安裝中，讓使用者無須進行先前在 SQL Server 2016 R Services中所需的升級步驟。 MicrosoftML 能提供最先進的機器學習演算法及資料轉換，可在遠端計算內容中調整或執行。 演算法包括可自訂的深度神經網路、快速決策樹及決策樹系、線性迴歸，以及羅吉斯迴歸。  |

### <a name="python-integration-for-in-database-analytics"></a>適用於資料庫內分析的 Python 整合

Python 語言能針對各種不同的機器學習工作提供絕佳的彈性和功能。 適用於 Python 的開放原始碼程式庫包括適用於可自訂類神經網路的數個平台，以及適用於自然語言處理的熱門程式庫。 

因為 Python 是與資料庫引擎整合，所以您可以在接近資料的情況下進行分析，並免去和資料移動相關的成本與安全性風險。 您可以使用如 Visual Studio 的工具來部署以 Python 為基礎的機器學習解決方案。 您的生產環境應用程式可以使用 SQL Server 資料存取方法，從 Python 3.5 執行階段取得預測、模型或視覺效果。

T-SQL 和 Python 整合可透過 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) \(部分機器翻譯\) 系統預存程序來支援。 您可以使用此預存程序來呼叫任何 Python 程式碼。 程式碼會在安全的雙重架構中執行，這可讓您以企業級的方式部署 Python 模型和指令碼，並可透過簡單的預存程序從應用程式中呼叫它們。 透過將資料從 SQL 串流到 Python 處理序及 MPI 通道平行處理，便能達成額外的效能提升。

您可以使用 T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) 函數，對先前以必要的二進位格式儲存的預先定型模型執行[原生評分](predictions/native-scoring-predict-transact-sql.md)。

### <a name="python-libraries"></a>Python 程式庫

| Package | 描述 |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| 相對於 RevoScaleR 的 Python 對等項目。 您可以針對線性及羅吉斯迴歸、決策樹、增強樹，以及隨機樹建立 Python 模型；它們全都可以平行化，也能在遠端計算內容中執行。 此套件支援使用多個資料來源和遠端計算內容。 資料科學家或開發人員可以在遠端 SQL Server 上執行 Python 程式碼，以在不移動資料的情況下探索資料或建置模型。 |
|[**microsoftml**](python/ref-py-microsoftml.md) |MicrosoftML R 套件的 Python 對等項目。 |

### <a name="pre-trained-models"></a>預先定型的模型

[**預先定型模型**](install/sql-pretrained-models-install.md)可供 Python 和 R 使用。使用這些模型來進行影像辨識和正負面情感分析，以根據您自己的資料產生預測。 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>在 SQL Server 安裝程式中將獨立伺服器作為共用功能

此版本也新增 [SQL Server 機器學習伺服器 (獨立式)](r/r-server-standalone.md)，此為完全獨立的資料科學伺服器，支援以 R 和 Python 進行統計和預測性分析。 和 R Services相同，此伺服器是下一版的 SQL Server 2016 R Server (獨立式)。 在使用獨立伺服器的情況下，您可以在不相依於 SQL Server 的情況下散發及調整 R 或 Python 解決方案。
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2016"></a>SQL Server 2016 的新功能

此版本透過 **SQL Server 2016 R Services** 將機器學習功能引進 SQL Server；此資料庫內分析引擎能在資料庫引擎執行個體內的常駐資料上處理 R 指令碼。

此外，發佈 **SQL Server 2016 R Server (獨立式)** 的目的是要提供在 Windows 伺服器上安裝 R Server 的方式。 一開始，SQL Server 安裝程式是在 Windows 上安裝 R Server 的唯一方式。 在後續版本中，想要在 Windows 上取得 R Server 的開發人員和資料科學家則可以使用另一個獨立安裝程式來達成相同的目標。 SQL Server 中的獨立伺服器，與獨立伺服器產品 [Microsoft R Server for Windows](/machine-learning-server/install/r-server-install-windows) \(英文\) 在功能上是一模一樣的。

如需完整的功能公告，請參閱 [SQL Server 2016 的新功能](../sql-server/what-s-new-in-sql-server-2016.md)。

| 版本 |功能更新 |
|---------|----------------|
| CU 新增項目 | [**即時評分**](predictions/real-time-scoring.md)會仰賴原生 C++ 程式庫來讀取以最佳化二進位格式儲存的模型，然後在不需要呼叫 R 執行階段的情況下產生預測。 這可讓評分作業變得更加快速。 透過使用即時評分，您可以從 R 程式碼執行預存程序或執行即時評分。 即時評分也可供 SQL Server 2016 使用，前提是執行個體必須已升級到最新版本的 [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]。 |
| 初始版本 | [**適用於資料庫內分析的 R 整合**](r/sql-server-r-services.md)。 <br/><br/> 用來以 T-SQL 呼叫 R 函數 (反之亦然) 的 R 套件。 RevoScaleR 函數能透過將資料區塊化成元件部分、協調及管理分散式處理，以及將結果彙總，來提供大規模的 R 分析。 在 SQL Server 2016 R Services (資料庫內) 中，RevoScaleR 引擎會與資料庫引擎執行個體整合，並在相同的處理內容中將資料和分析整合在一起。 <br/><br/>T-SQL 和 R 是透過 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) \(部分機器翻譯\) 進行整合。 您可以使用此預存程序來呼叫任何 R 程式碼。 這個安全的基礎結構可讓您以企業級的方式部署 R 模型和指令碼，並可透過簡單的預存程序從應用程式中呼叫它們。 透過將資料從 SQL 串流到 R 處理序及 MPI 通道平行處理，便能達成額外的效能提升。 <br/><br/>您可以使用 T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) 函數，對先前以必要的二進位格式儲存的預先定型模型執行[原生評分](predictions/native-scoring-predict-transact-sql.md)。|

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="linux-support"></a>Linux 支援

SQL Server 2019 會在您安裝具有資料庫引擎執行個體的機器學習套件時，新增適用於 R 和 Python 的 Linux 支援。 如需詳細資訊，請參閱[在 Linux 上安裝 SQL Server 機器學習服務](../linux/sql-server-linux-setup-machine-learning.md)。

在 Linux 上，SQL Server 2017 不會有 R 或 Python 整合，但您可以在 Linux 上使用[原生評分](predictions/native-scoring-predict-transact-sql.md)，因為該功能是透過 (可在 Linux 上執行的) T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) 提供。 原生評分可從預先定型的模型中進行高效能的評分，而不需要呼叫甚至要求 R 執行階段。
::: moniker-end

## <a name="next-steps"></a>後續步驟

+ [安裝 SQL Server 機器學習服務 (資料庫內)](install/sql-machine-learning-services-windows-install.md)
