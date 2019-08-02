---
title: SQL Server Machine Learning 服務 (R、Python) 的總覽
description: 概述 SQL Server 中的 Machine Learning Services 功能, 您可以在其中整合 Python 和 R 與資料科學的關聯式資料、統計模型、機器學習模型、預測性分析、資料視覺效果等等。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/24/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4ab4cd7c93cfd1a98a819a849e643d590450cd28
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714675"
---
# <a name="sql-server-machine-learning-services-r-python"></a>SQL Server Machine Learning 服務 (R、Python)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Machine Learning Services 是 SQL Server 的功能, 可用來執行資料庫內 R 和 Python 腳本。 此功能包括適用于高效能預測性分析和機器學習的[Microsoft R 和 Python 套件](#components)。 關聯式資料可透過預存程式、包含 R 和 Python 語句的 T-sql 腳本, 或包含 T-sql 的 R 和 Python 程式碼, 用於 R 和 Python 腳本中。

在 Azure SQL Database 中, [Machine Learning 服務 (使用 R)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview)目前為公開預覽狀態。

## <a name="bring-compute-power-to-the-data"></a>將計算能力帶到資料

Machine Learning 服務的關鍵價值主張是其企業 R 和 Python 套件的強大功能, 以提供大規模的先進分析, 並能夠將計算和處理功能帶入資料所在的位置, 而不需要將資料提取到網路。 這可提供多項優點:

+ 資料安全性。 讓 R 和 Python 的執行更接近資料來源, 可以避免浪費或不安全的資料移動。
+ 速度。 資料庫已針對集合型操作進行最佳化。 資料庫的最新創新 (例如記憶體內部資料表) 讓摘要和匯總得以閃電, 而且是資料科學的絕佳補充。
+ 簡化部署和整合。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]是許多其他資料管理工作和應用程式之作業的中心點。 藉由使用位於資料庫或報表倉儲中的資料, 您可以確保機器學習解決方案所使用的資料是一致且最新的。 
+ 跨雲端和內部部署的效率。 您可以依賴企業資料管線, 包括[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]和 Azure Data Factory, 而不是在 R 或 Python 會話中處理資料。 透過 Power BI 或 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 很容易就能報告結果或分析。

資料科學家和開發人員可以使用正確的 SQL 和 R 組合，來進行不同的資料處理和分析工作，因此更有效率。

<a name="components"></a>

## <a name="components"></a>元件

SQL Server 支援 R 和 Python。 下表描述這些元件。

| 元件 | 描述 |
|-----------|-------------|
| SQL Server Launchpad 服務 | 管理外部 R 和 Python 執行時間與 database engine 實例之間通訊的服務。 |
| R 套件 | [**RevoScaleR**](r/ref-r-revoscaler.md)是可調整 R 的主要程式庫。此程式庫中的函式是最廣泛使用的功能之一。 在這些程式庫中可找到資料轉換和操作、統計摘要、視覺效果, 以及許多形式的模型化和分析。 此外, 這些程式庫中的函式會自動將工作負載分散到可用的核心, 以進行平行處理, 並且能夠處理由計算引擎協調和管理的資料區塊。  <br/>[**MicrosoftML (R)** ](r/ref-r-microsoftml.md)新增機器學習演算法, 以建立文字分析、影像分析和情感分析的自訂模型。 <br/>[**sqlRUtils**](r/ref-r-sqlrutils.md)提供 helper 函式, 可將 R 腳本放入 t-sql 預存程式、向資料庫註冊預存程式, 以及從 R 開發環境執行預存程式。<br/>[**olapR**](r/ref-r-olapr.md)是用來在 R 腳本中建立或執行 MDX 查詢。|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open)是 Microsoft 的 R 開放原始碼散發。包含封裝和解譯器。 請一律使用安裝程式所安裝的 MRO 版本。 |
| R 工具 | R 主控台視窗和命令提示字元是 R 散發套件中的標準工具。  |
| R 範例和腳本 |  開放原始碼 R 和 RevoScaleR 套件包含內建的資料集, 讓您可以使用預先安裝的資料來建立和執行腳本。 |
| Python 套件 | [**revoscalepy**](python/ref-py-revoscalepy.md)是可調整 Python 的主要程式庫, 其中包含用於資料操作、轉換、視覺化和分析的功能。 <br/>[**microsoftml (Python)** ](python/ref-py-microsoftml.md)新增機器學習演算法, 以建立文字分析、影像分析和情感分析的自訂模型。  |
| Python 工具 | 內建的 Python 命令列工具適用于臨機操作測試和工作。  |
| Anaconda | Anaconda 是 Python 和基本套件的開放原始碼散發。 |
| Python 範例和腳本 | 如同 R, Python 包含內建的資料集和腳本。  |
| R 和 Python 中預先定型的模型 | 預先定型的模型是針對特定使用案例所建立, 並由 Microsoft 的資料科學工程團隊進行維護。 您可以使用您所提供的新資料輸入, 依實際情況使用預先定型的模型來對文字中的正負情感進行評分, 或偵測影像中的特徵。 模型會在 Machine Learning 服務中執行, 但是無法透過 SQL Server 安裝程式安裝。 如需詳細資訊, 請參閱[在 SQL Server 上安裝預先定型的機器學習模型](install/sql-pretrained-models-install.md)。 |

## <a name="using-sql-mls"></a>使用 SQL MLS

開發人員和分析師通常會在本機 SQL Server 實例上執行程式碼。 藉由加入 Machine Learning 服務並啟用外部腳本執行, 您就能夠在 SQL Server 形式: 在預存程式中包裝腳本、在 SQL Server 資料表中儲存模型, 或結合 T-sql 和 R 或 Python 函式, 以執行 R 和 Python 程式碼在查詢中。

腳本執行是在資料安全性模型的界限內: 關係資料庫的許可權是腳本中資料存取的基礎。 執行 R 或 Python 腳本的使用者, 不能在 SQL 查詢中使用該使用者無法存取的任何資料。 您需要標準資料庫的 [讀取] 和 [寫入] 許可權, 再加上執行外部腳本的額外許可權。 您針對關聯式資料撰寫的模型和程式碼會包裝在預存程式中, 或序列化為二進位格式並儲存在資料表中, 或在您將原始位元組資料流程序列化為檔案時, 從磁片載入。

資料庫內分析最常見的方法是使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), 傳遞 R 或 Python 腳本做為輸入參數。

傳統的用戶端-伺服器互動是另一種方法。 從任何具有 IDE 的用戶端工作站, 您都可以安裝[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)或[Python 程式庫](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter), 然後撰寫程式碼, 將執行 (稱為*遠端計算內容*) 推送至遠端 SQL Server 的資料和作業。 

最後, 如果您使用[獨立伺服器](r/r-server-standalone.md)和開發人員版本, 您可以使用相同的程式庫和解譯器在用戶端工作站上建立解決方案, 然後在 SQL Server Machine Learning 服務 (資料庫內) 上部署生產環境程式碼。 

## <a name="how-to-get-started"></a>如何開始使用

### <a name="step-1-install-the-software"></a>步驟 1：安裝軟體

+ [SQL Server Machine Learning 服務 (資料庫內)](install/sql-machine-learning-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>步驟 2：設定開發工具

資料科學家通常會在自己的膝上型電腦或開發工作站上使用 R 或 Python, 以流覽資料, 並建立和調整預測模型, 直到達到良好的預測模型為止。 透過 SQL Server 中的資料庫內分析, 不需要變更此程式。 安裝完成之後, 您可以在本機和遠端執行 R 或 Python 程式碼 SQL Server。

![rsql_keyscenario2](r/media/rsql-keyscenario2.png) 

+ **使用您偏好的 IDE**。 您可以將 R 和 Python 程式庫連結至您所選擇的開發工具。 如需詳細資訊, 請參閱[設定 R 工具](r/set-up-a-data-science-client.md)和[設定 Python 工具](python/setup-python-client-tools-sql.md)。  

+ **從遠端或本機工作**。 資料科學家可以連接到 SQL Server, 並如往常般將資料帶入用戶端進行本機分析。 不過, 更好的解決方案是使用**RevoScaleR**或**revoscalepy** api, 將計算推送至 SQL Server 的電腦, 避免成本高昂且不安全的資料移動。

+ **在 SQL Server 預存程式中內嵌 R 或 Python 腳本**。 當您的程式碼完全優化時, 請將它包裝在預存程式中, 以避免不必要的資料移動和優化資料處理工作。

### <a name="step-3-write-your-first-script"></a>步驟 3：撰寫您的第一個腳本

從 T-sql 腳本中呼叫 R 或 Python 函式:

+ [R瞭解使用 R 的資料庫內分析](tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [R使用 R 的端對端逐步解說](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
+ [Python使用 T-sql 執行 Python](tutorials/run-python-using-t-sql.md)
+ [Python瞭解使用 Python 的資料庫內分析](tutorials/sqldev-in-database-python-for-sql-developers.md)

選擇工作的最佳語言。 R 適用于難以使用 SQL 來執行的統計計算。 對於資料的集合型作業, 請利用 SQL Server 的威力來達到最大效能。 使用記憶體內部資料庫引擎, 以快速計算資料行。

### <a name="step-4-optimize-your-solution"></a>步驟 4：優化您的解決方案

當模型準備好要調整企業資料時, 資料科學家通常會與 DBA 或 SQL 開發人員合作, 以將程式優化, 例如:

+ 特徵工程
+ 資料內嵌和資料轉換
+ 計分

傳統上, 使用 R 的資料科學家在效能和規模方面都有問題, 尤其是在使用大型資料集時。 這是因為一般執行時間的執行是單一執行緒, 而且只能容納符合本機電腦上可用記憶體的資料集。 與 SQL Server Machine Learning 服務整合可提供多項功能以獲得更好的效能, 以及更多的資料:

+ **RevoScaleR**:此 R 套件包含一些最受歡迎的 R 函式的執行, 經過重新設計可提供平行處理和調整。 此套件也包含可進一步提升效能和規模的功能, 方法是將計算推送到 SQL Server 電腦, 這通常會有更高的記憶體和計算能力。

+ **revoscalepy**。 此 Python 程式庫會在 RevoScaleR 中執行最受歡迎的功能, 例如遠端計算內容, 以及許多支援分散式處理的演算法。

如需效能的詳細資訊, 請參閱此[效能案例研究](r/performance-case-study-r-services.md)和[R 和資料優化](r/r-and-data-optimization-r-services.md)。

### <a name="step-5-deploy-and-consume"></a>步驟 5：部署和使用

在腳本或模型可供生產環境使用之後, 資料庫開發人員可能會在預存程式中內嵌程式碼或模型, 以便從應用程式呼叫儲存的 R 或 Python 程式碼。 從 SQL Server 儲存和執行 R 程式碼有許多優點: 您可以使用方便的 SQL Server 介面, 而且所有計算都會在資料庫中進行, 以避免不必要的資料移動。

![rsql_keyscenario1](r/media/rsql-keyscenario1.png)

+ **安全且可擴充**。 SQL Server 使用新的擴充性架構, 讓您的資料庫引擎保持安全, 並隔離 R 和 Python 會話。 您也可以控制可執行腳本的使用者, 也可以指定程式碼可以存取的資料庫。 您可以控制配置給執行時間的資源數量, 以防止大量計算危害整體伺服器效能。

+ **排程與審核**。 當外部腳本作業在 SQL Server 中執行時, 您可以控制和審核資料科學家所使用的資料。 您也可以排程工作並撰寫包含外部 R 或 Python 腳本的工作流程, 就像排程任何其他 T-sql 作業或預存程式一樣。

若要利用 SQL Server 中的資源管理和安全性功能, 部署程式可能包含下列工作:

+ 將程式碼轉換成可在預存程式中以最佳方式執行的函式
+ 設定安全性和鎖定特定工作所使用的套件
+ 啟用資源管理 (需要 Enterprise edition)

如需詳細資訊, 請參閱[r 的資源管理](r/resource-governance-for-r-services.md)和適用[于 SQL Server 的 r 套件管理](r/install-additional-r-packages-on-sql-server.md)。

## <a name="portability-and-related-products"></a>可攜性和相關產品

自訂 R 和 Python 程式碼的可攜性是透過內建于多個產品的封裝散發和解譯器來定址。 隨附于 SQL Server 的相同套件也適用于數個其他 Microsoft 產品和服務, 包括稱為[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/)的非 SQL 版本。 

包含 R 和 Python 解譯器的免費用戶端是[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)和[python 程式庫](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)。

在 Azure 上, 您也可以在 Azure Machine Learning、 [HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview)和 azure[虛擬機器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux)等 azure 服務上, 取得 Microsoft 的 R 和 Python 套件和解譯器。 [資料科學虛擬機器](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)包括具有多個廠商工具的完整開發工作站, 以及 Microsoft 的程式庫和解譯器。

## <a name="see-also"></a>另請參閱

[安裝 SQL Server Machine Learning 服務](install/sql-machine-learning-services-windows-install.md)
