---
title: 機器學習服務在 SQL Server |Microsoft Docs
description: 概觀簡介 SQL Server 2017 Machine Learning 服務、 R 和 Python 支援在資料庫內分析
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/27/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6f29867351f0fa19817c7f39cbcca5da96a7e862
ms.sourcegitcommit: 010755e6719d0cb89acb34d03c9511c608dd6c36
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240186"
---
# <a name="machine-learning-services-in-sql-server-2017"></a>機器學習服務中的 SQL Server 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2017 Machine Learning 服務是 database engine 執行個體，用於執行 SQL Server 上的 R 和 Python 程式碼的附加元件。 與核心引擎處理序隔離，但預存程序、 T-SQL 指令碼包含 R 或 Python 的陳述式，或包含 T-SQL 中的 R 或 Python 程式碼的關聯式資料完全可供使用的擴充性架構中，執行程式碼。 

如果您先前使用 SQL Server 2016 R Services，SQL Server 2017 中的 Machine Learning 服務是新一代的 R 支援的基底 R、 RevoScaleR、 MicrosoftML 及 2016年中引進的其他程式庫的更新版本。

Machine Learning 服務的主要價值主張是其企業 R 和 Python 套件的乘冪，以提供進階的分析，在小數位數，並且能夠讓計算和處理資料的所在，不必在提取資料在網路中。

## <a name="components"></a>Components

SQL Server 2017 支援 R 和 Python。 下表描述的元件。

| 元件 | 描述 |
|-----------|-------------|
| SQL Server Launchpad 服務 | 管理外部 R 和 Python 執行階段和資料庫引擎執行個體之間的通訊服務。 |
| R 套件 | [**RevoScaleR** ](r/revoscaler-overview.md)是主要的程式庫，此程式庫中的可調整 r 函數是使用最廣泛。 這些程式庫中找到資料轉換和操作、 統計摘要、 視覺化和模型化和分析的許多形式。 此外，這些程式庫中的函式會自動將工作負載分散到可用的核心進行平行處理，能夠協調及計算引擎所管理的資料區塊上運作。  <br/>[**MicrosoftML (R)** ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)新增機器學習演算法來建立自訂文字分析、 影像分析和情緒分析模型。 <br/>[**sqlRUtils** ](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)提供 helper 函式將 R 指令碼放入 T-SQL 預存程序、 註冊預存程序使用資料庫時，以及從 R 開發環境執行預存程序。<br/>[**olapR** ](r/how-to-create-mdx-queries-using-olapr.md)適用於建置或執行 R 指令碼中的 MDX 查詢。|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open)是 Microsoft 的開放原始碼散發套件的。會包含封裝和解譯器。 一律使用 MRO 安裝程式安裝的版本。 |
| R 工具 | R 主控台視窗和命令提示字元是標準的工具，在 R 散發。  |
| R 範例和指令碼 |  開放原始碼 R 和 RevoScaleR 套件包含內建的資料集，讓您可以建立並使用預先安裝的資料執行指令碼。 |
| Python 套件 | [**revoscalepy** ](python/what-is-revoscalepy.md)可延展的 Python 與資料操作、 轉換、 視覺化和分析的函式中為主要媒體櫃。 <br/>[**microsoftml (Python)** ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)新增機器學習演算法來建立自訂文字分析、 影像分析和情緒分析模型。  |
| Python 工具 | 內建的 Python 命令列工具可用於臨機操作測試和工作項目。  |
| Anaconda | Anaconda 是開放原始碼散發套件的 Python 和基本封裝。 |
| Python 範例和指令碼 | 在使用 R、 Python 會包含內建的資料集與指令碼。  |
| 預先定型的模型，在 R 和 Python | 預先定型的模型建立的特定使用案例，並由 Microsoft 的資料科學工程小組所維護。 您可以使用預先定型的模型，以-為評分正負面情感的文字，或在映像，使用您提供的新資料輸入中偵測功能。 模型會在機器學習服務中執行，但無法透過 SQL Server 安裝程式安裝。 如需詳細資訊，請參閱 <<c0> [ 安裝的預先定型的機器學習服務模型在 SQL Server 上的](install/sql-pretrained-models-install.md)。 |

## <a name="using-sql-mls"></a>使用 SQL MLS

開發人員和分析師通常會有在本機的 SQL Server 執行個體上執行的程式碼。 藉由新增機器學習服務，然後啟用外部指令碼執行，您可以在 SQL 伺服器型態執行 R 和 Python 程式碼的能力： 包裝在預存程序的指令碼、 將模型儲存在 SQL Server 資料表中，或結合 T-SQL 和 R 或 Python 函式在查詢中。

在資料庫內分析的最常見方法是使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，傳遞做為輸入參數的 R 或 Python 指令碼。

典型主從式的互動為另一種方法。 從任何具有 IDE 的用戶端工作站，您可以安裝[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)或[Python 程式庫](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)，然後撰寫推送執行的程式碼 (稱為*遠端計算內容*) 資料與遠端的 SQL Server 的作業。 

最後，如果您使用[獨立伺服器](r/r-server-standalone.md)和 Developer edition 中，您可以建置使用相同的程式庫和解譯器，在用戶端工作站上的解決方案，然後再部署 SQL Server Machine Learning 上的實際執行程式碼服務 （資料庫）。 

## <a name="how-to-get-started"></a>如何開始使用

### <a name="step-1-install-the-software"></a>步驟 1： 安裝軟體

+ [SQL Server Machine Learning 服務 （資料庫）](install/sql-machine-learning-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>步驟 2： 設定開發工具

資料科學家通常使用 R 或 Python 自己的膝上型電腦或開發工作站上，瀏覽資料，以及建置和微調預測模型，直到達成良好的預測模型。 使用 SQL Server 中的資料庫內分析，還有不需要變更此程序。 安裝完成後，您可以執行 R 或 Python 程式碼，在 SQL Server 上本機和遠端即可。

![rsql_keyscenario2](r/media/rsql-keyscenario2.png) 

+ **使用您偏好的 IDE**。 您可以連結的 R 和 Python 程式庫至您所選的開發工具。 如需詳細資訊，請參閱 <<c0> [ 設定 R 工具](r/set-up-a-data-science-client.md)並[設定 Python 工具](python/setup-python-client-tools-sql.md)。  

+ **使用遠端或本機**。 資料科學家可以連線到 SQL Server，並將資料帶給用戶端進行本機分析，如往常般。 不過，較好的解決方案是使用**RevoScaleR**或是**revoscalepy** Api，將計算推送到 SQL Server 電腦，避免成本高同時不安全的資料移動。

+ **在 SQL Server 預存程序中內嵌 R 或 Python 指令碼**。 當您的程式碼完全最佳化時，請將它包裝在預存程序中，以避免不必要的資料移動，並最佳化資料處理工作。

### <a name="step-3-write-your-first-script"></a>步驟 3： 撰寫您的第一個指令碼

呼叫 R 或 Python 函式從 T-SQL 指令碼內：

+ [： 了解使用 R 的資料庫內分析](tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [為： 以 R 端對端逐步解說](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
+ [Python：使用 T-SQL 執行 Python](tutorials/run-python-using-t-sql.md)
+ [Python： 了解使用 Python 的資料庫內分析](tutorials/sqldev-in-database-python-for-sql-developers.md)

選擇工作的最佳語言。 R 是最適合使用 SQL 實作困難的統計計算。 資料的集合式作業，利用強大的 SQL Server，以達到最大效能。 使用記憶體中資料庫引擎進行非常快速的計算資料行。

### <a name="step-4-optimize-your-solution"></a>步驟 4： 最佳化您的解決方案

備妥可調整的企業資料模型時，資料科學家通常適用於 DBA 或 SQL 開發人員最佳化程序，例如︰

+ 特徵工程
+ 資料擷取和資料轉換
+ 計分

傳統上，使用 R 的資料科學家有問題的效能和延展性，尤其是使用大型資料集。 這是因為通用執行階段實作是單一執行緒，而且可以容納放入本機電腦上的可用記憶體的資料集。 與 SQL Server Machine Learning 服務整合會提供多項功能，以提升效能、 更多資料：

+ **RevoScaleR**： 此 R 封裝包含一些最受歡迎的 R 函數，經過重新設計可提供平行處理與延展的實作。 此封裝也會包含進一步提升效能與延展性，藉由將計算推送到 SQL Server 電腦，它通常記憶體更大且運算能力的函式。

+ **revoscalepy**。 此 Python 程式庫實作 RevoScaleR，在遠端計算內容，例如最受歡迎的函式和許多支援的演算法分散式處理。

如需有關效能的詳細資訊，請參閱此[效能案例研究](r/performance-case-study-r-services.md)並[R 和資料最佳化](r/r-and-data-optimization-r-services.md)。

### <a name="step-5-deploy-and-consume"></a>步驟 5： 部署和取用

指令碼或模型可供生產環境使用之後，資料庫開發人員可能會嵌入程式碼或模型的預存程序，以便可以從應用程式呼叫的已儲存的 R 或 Python 程式碼。 儲存並執行從 SQL Server 的 R 程式碼有許多優點： 您可以使用方便的 SQL Server 介面，而且在資料庫中，避免不必要的資料移動的所有計算都進行。

![rsql_keyscenario1](r/media/rsql-keyscenario1.png)

+ **安全且可擴充**。 SQL Server 會使用新的擴充性架構，保持您資料庫引擎的安全，並隔離 R 和 Python 的工作階段。 您也可以控制可以執行指令碼的使用者，您可以指定可以存取的程式碼的資料庫。 您可以控制配置給執行階段，以避免大量計算危及整體伺服器效能的資源數量。

+ **排程和稽核**。 當 SQL Server 中執行外部指令碼工作時，您可以控制和稽核資料科學家所使用的資料。 您也可以排定工作並撰寫包含外部的 R 或 Python 指令碼，就像任何其他的 T-SQL 作業或預存程序，您會排程工作流程。

若要利用的資源管理和安全性功能的 SQL Server 中，部署程序可能包括下列工作：

+ 將您的程式碼轉換成可以在預存程序中以最佳方式執行的函式
+ 設定安全性和鎖定在特定工作所使用的套件
+ 啟用資源控管 （需要 Enterprise edition）

如需詳細資訊，請參閱 <<c0> [ 適用於 R 的資源控管](r/resource-governance-for-r-services.md)並[SQL Server 的 R 封裝管理](r/install-additional-r-packages-on-sql-server.md)。

## <a name="version-history"></a>版本歷程記錄

SQL Server 2017 Machine Learning 服務是新一代的 SQL Server 2016 R Services，加強可包含 Python。 下表是所有的產品版本，從開始到目前版本的完整清單。 

| 產品名稱 | 引擎版本 | 發行日期 |
|--------------|---------|--------------|
| SQL Server 2017 Machine Learning 服務 （資料庫） | R Server 9.2.1 <br/> Python 伺服器 9.2 | 2017 年 10 月 |
| SQL Server 2017 Machine Learning 伺服器 （獨立式） | R Server 9.2.1 <br/> Python 伺服器 9.2 | 2017 年 10 月 |
| SQL Server 2016 R Services （資料庫） | R Server 9.1  | 2017 年 7 月  |
| SQL Server 2016 R Server （獨立式）  |  R Server 9.1 | 2017 年 7 月 |

如需版本的套件版本，請參閱對應中的版本[升級 R 和 Python 元件](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md#version-map)。

## <a name="portability-and-related-products"></a>可攜性及相關的產品

可攜性的自訂 R 和 Python 程式碼會處理透過套件發佈和多項產品內建的解譯器。 相同的套件隨附於 SQL Server 中也會有數個其他 Microsoft 產品和服務，包括非 SQL 版本，稱[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/)。 

免費包含我們的 R 和 Python 解譯器的用戶端[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)並[Python 程式庫](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)。

在 Azure 上 Microsoft R 和 Python 套件和解譯器也會提供在 Azure Machine Learning 和 Azure 服務，例如[HDInsight](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-on-azure-hdinsight)，並[Azure 虛擬機器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux)。 [資料科學虛擬機器](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)包括從多個供應商，以及程式庫的工具與 microsoft 的解譯器的配備完畢，可以的開發工作站。

## <a name="see-also"></a>另請參閱

[安裝 SQL Server Machine Learning 服務](install/sql-machine-learning-services-windows-install.md)