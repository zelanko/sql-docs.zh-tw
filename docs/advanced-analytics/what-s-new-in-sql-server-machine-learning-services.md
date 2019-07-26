---
title: 新功能 |Microsoft Docs
description: SQL Server 2016 R Services、R Server SQL Server 2017 Machine Learning Services 的每個版本都有新的功能公告。
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: c466c7e039e515be4ef65b4f5680ece2e1d861a8
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468978"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning 服務的新功能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

機器學習功能會新增至每個版本中的 SQL Server, 因為我們會繼續擴充、擴充和加深資料平臺、先進分析和資料科學之間的整合。 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019-preview"></a>SQL Server 2019 preview 的新功能

此版本會在 SQL Server 中新增 R 和 Python 機器學習作業的最上層要求功能。 如需此版本中所有功能的詳細資訊, 請參閱[SQL Server 2019 中的新](../sql-server/what-s-new-in-sql-server-ver15.md)功能和[SQL Server 2019 的版本](../sql-server/sql-server-ver15-release-notes.md)資訊。

> [!NOTE]
> 如需 SQL Server 2019 中的 JAVA 新功能檔, 請參閱[SQL Server 語言擴充功能有哪些新功能？](https://docs.microsoft.com/sql/language-extensions/language-extensions-whats-new)

| 版本 | 功能更新 |
|---------|----------------|
| CTP 3.0 | 無變更。 |
| CTP 2.5 | 無變更。 |
| CTP 2.4 | 適用于 R 和 Python 的[建立外部程式庫 (transact-sql)](../t-sql/statements/create-external-library-transact-sql.md)的 Linux 支援。 |
| CTP 2.3 | 在 Windows 上, 您可以使用[CREATE EXTERNAL library (transact-sql)](../t-sql/statements/create-external-library-transact-sql.md)語句, 在外部程式庫中存取 Python 程式碼。 |
| CTP 2.2 | 無變更。 |
| CTP 2.1 | 無變更。 |
| CTP 2.0 | 適用于 R 和 Python 機器學習的 Linux 平臺支援。 開始[在 Linux 上安裝 SQL Server Machine Learning 服務](../linux/sql-server-linux-setup-machine-learning.md)。 |
|  | [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)引進兩個新的參數, 可讓您輕鬆地從分割的資料產生多個模型。 在本教學課程中深入瞭解如何在[R 中建立以資料分割為基礎的模型](tutorials/r-tutorial-create-models-per-partition.md)。 |
|   | Windows 和 Linux 現在都支援容錯移轉叢集支援, 假設所有節點上都已啟動 SQL Server Launchpad 服務。 如需詳細資訊, 請參閱[SQL Server 容錯移轉叢集安裝](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)。 |

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>SQL Server 2017 中的新功能

此版本新增[Python 支援和領先業界的機器學習服務演算法](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)。 已重新命名以反映新的範圍, SQL Server 2017 標示[SQL Server Machine Learning 服務 (資料庫內)](what-is-sql-server-machine-learning.md)的引進, 同時提供 Python 和 R 的語言支援。 

如需全部功能公告, 請參閱[SQL Server 2017 中的新](../sql-server/what-s-new-in-sql-server-2017.md)功能。

### <a name="r-enhancements"></a>R 增強功能

SQL Server 2017 Machine Learning 服務的 R 元件是下一代的 SQL Server 2016 R 服務, 其中包含基底 R、RevoScaler 和其他封裝的更新版本。

R 的新功能包括[**套件管理**](r/install-additional-r-packages-on-sql-server.md), 並具有下列重點: 

+ 資料庫角色可協助 Dba 管理封裝, 以及指派套件安裝的許可權。
+ [建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)可協助 dba 以熟悉的 t-sql 語言來管理套件。
+ [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md)函數可協助安裝、移除或列出使用者所擁有的套件。 如需詳細資訊, 請參閱[如何使用 RevoScaleR 函數在 SQL Server 上尋找或安裝 R 套件](r/use-revoscaler-to-manage-r-packages.md)。

### <a name="r-libraries"></a>R 程式庫

| 套件 | 描述 |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | 在此版本中, MicrosoftML 包含在預設的 R 安裝中, 可排除先前 SQL Server 2016 R 服務中所需的升級步驟。 MicrosoftML 提供最先進的機器學習演算法和資料轉換, 可以在遠端計算內容中進行調整或執行。 演算法包括可自訂的深度類神經網路、快速決策樹和決策樹系、線性回歸和羅吉斯回歸。  |

### <a name="python-integration-for-in-database-analytics"></a>資料庫內分析的 Python 整合

Python 是一種語言, 為各種機器學習工作提供絕佳的彈性和強大功能。 適用于 Python 的開放原始碼程式庫包含數個可自訂類神經網路的平臺, 以及適用于自然語言處理的熱門程式庫。 現在, SQL Server 2017 Machine Learning 支援這種廣泛使用的語言。

由於 Python 已與資料庫引擎整合, 因此您可以保持接近資料的分析, 並消除與資料移動相關聯的成本和安全性風險。 您可以使用 Visual Studio 之類的工具, 部署以 Python 為基礎的機器學習解決方案。 您的生產應用程式可以使用 SQL Server 資料存取方法, 從 Python 3.5 執行時間取得預測、模型或視覺效果。

T-sql 和 Python 整合是透過[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系統預存程式來支援。 您可以使用這個預存程式來呼叫任何 Python 程式碼。 程式碼會在安全的雙重架構中執行, 可讓您使用簡單的預存程式, 從應用程式呼叫 Python 模型和腳本的企業級部署。 將 SQL 的資料串流處理至 Python 進程和 MPI 通道平行化, 即可達到額外的效能提升。

您可以使用 T-sql [PREDICT](../t-sql/queries/predict-transact-sql.md)函數, 在先前以必要的二進位格式儲存的預先定型模型上執行[原生評分](sql-native-scoring.md)。

### <a name="python-libraries"></a>Python 程式庫

| 套件 | 描述 |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| Python-等同于 RevoScaleR。 您可以建立線性和羅吉斯回歸、決策樹、推進式樹狀結構和隨機樹系的 Python 模型、所有可並行, 而且能夠在遠端計算內容中執行。 此套件支援使用多個資料來源和遠端計算內容。 資料科學家或開發人員可以在遠端 SQL Server 上執行 Python 程式碼, 以流覽資料或建立模型, 而不需要移動資料。 |
|[**microsoftml**](python/ref-py-microsoftml.md) |Python-等同于 MicrosoftML R 套件。 |

### <a name="pre-trained-models"></a>預先定型的模型

[**預先定型的模型**](install/sql-pretrained-models-install.md)適用于 Python 和 R。請使用這些模型進行影像辨識和正負面的情感分析, 以在您自己的資料上產生預測。 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>獨立伺服器做為 SQL Server 安裝程式中的共用功能

此版本也新增了[SQL Server Machine Learning Server (獨立式)](r/r-server-standalone.md), 這是完全獨立的資料科學伺服器, 可支援 R 和 Python 中的統計和預測性分析。 如同 R Services, 此伺服器是下一版的 SQL Server 2016 R Server (獨立式)。 使用獨立伺服器, 您可以散發和調整 R 或 Python 解決方案, 而不需要 SQL Server 的相依性。
::: moniker-end

## <a name="new-in-sql-server-2016"></a>SQL Server 2016 中的新功能

此版本引進了機器學習功能, 可透過**SQL Server 2016 R 服務**SQL Server, 這是一個資料庫內的分析引擎, 用於處理資料庫引擎實例內常駐資料的 R 腳本。

此外, **SQL Server 2016 r server (獨立式)** 已發行為在 Windows 伺服器上安裝 R server 的方法。 一開始, SQL Server 安裝程式會提供安裝適用于 Windows R 伺服器的唯一方式。 在較新的版本中, 需要 Windows 上 R 伺服器的開發人員和資料科學家可以使用另一個獨立安裝程式來達到相同的目標。 SQL Server 中的獨立伺服器在功能上等同于獨立伺服器產品, 也就是[適用于 Windows 的 Microsoft R server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

如需全部功能公告, 請參閱[SQL Server 2016 中的新](../sql-server/what-s-new-in-sql-server-2016.md)功能。

| 版本 |功能更新 |
|---------|----------------|
| CU 新增 | [**即時計分**](real-time-scoring.md)依賴原生C++程式庫來讀取以優化二進位格式儲存的模型, 然後產生預測, 而不需要呼叫 R 執行時間。 這可讓評分作業的速度更快。 使用即時評分, 您可以執行預存程式, 或從 R 程式碼執行即時評分。 如果實例升級至最新版本的[!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)], 則 SQL Server 2016 也可以使用即時評分。 |
| 最初發行 | [**資料庫內分析的 R 整合**](r/sql-server-r-services.md)。 <br/><br/> 用來在 T-sql 中呼叫 R 函數的 r 封裝, 反之亦然。 RevoScaleR 函式會將資料區塊化成元件部分、協調和管理分散式處理, 以及匯總結果, 以提供大規模的 R 分析。 在 SQL Server 2016 R Services (資料庫內) 中, RevoScaleR 引擎會與資料庫引擎實例整合, 同時在相同的處理內容中看待資料和分析。 <br/><br/>T-sql 和 R 透過[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)整合。 您可以使用這個預存程式來呼叫任何 R 程式碼。 這個安全的基礎結構可讓您使用簡單的預存程式, 從應用程式呼叫 Rn 模型和腳本的企業級部署。 將 SQL 的資料串流處理至 R 進程和 MPI 通道平行化, 即可達到額外的效能提升。 <br/><br/>您可以使用 T-sql [PREDICT](../t-sql/queries/predict-transact-sql.md)函數, 在先前以必要的二進位格式儲存的預先定型模型上執行[原生評分](sql-native-scoring.md)。|

## <a name="linux-support-roadmap"></a>Linux 支援藍圖

當您使用 database engine 實例安裝機器學習服務套件時, SQL Server 2019 CTP 2.3 會新增適用于 R 和 Python 的 Linux 支援。 如需詳細資訊, 請參閱[在 Linux 上安裝 SQL Server Machine Learning 服務](../linux/sql-server-linux-setup-machine-learning.md)。

在 Linux 上, SQL Server 2017 不會有 R 或 Python 整合, 但您可以在 Linux 上使用[原生計分](sql-native-scoring.md), 因為這種功能可透過 t-sql [PREDICT](../t-sql/queries/predict-transact-sql.md)取得, 它是在 linux 上執行。 原生評分可從預先定型模型進行高效能的計分, 而不需要呼叫或甚至要求 R 執行時間。

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>Azure SQL Database 中的 Machine Learning 服務

Azure SQL Database 中的 Machine Learning 服務 (使用 R) 處於公開預覽狀態。 如需詳細資訊, 請參閱[使用 R Azure SQL Database Machine Learning 服務 (預覽)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview)。

## <a name="next-steps"></a>後續步驟

+ [安裝 SQL Server 2017 Machine Learning 服務 (資料庫內)](install/sql-machine-learning-services-windows-install.md)
+ [機器學習服務教學課程和範例](tutorials/machine-learning-services-tutorials.md)
