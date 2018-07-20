---
title: SQL Server Machine Learning 及 R Services （資料庫） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 05a2a17988912d7066b0d9f6bf398b889a3cd882
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174775"
---
# <a name="sql-server-machine-learning-and-r-services-in-database"></a>SQL Server Machine Learning 及 R Services （資料庫）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

資料庫中安裝的機器學習服務運作的 SQL Server 資料庫引擎執行個體，為您的 SQL Server 執行個體的常駐資料提供 R 和 Python 的外部指令碼支援的內容中。 因為與機器學習服務整合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以讓分析貼近資料，並排除與移動資料相關聯的安全性風險與成本。

因為資料庫引擎是多個執行個體，您可以安裝多個執行個體的資料庫內分析，或甚至是更舊版本和較新版本的並存。 選擇加入其中一個[SQL Server 2017 Machine Learning 服務 （資料庫）](../install/sql-machine-learning-standalone-windows-install.md)使用 R 和 Python，或[SQL Server 2016 R Services （資料庫）](../install/sql-r-standalone-windows-install.md)只 

機器學習服務元件也可以安裝為執行個體無關[獨立伺服器](r-server-standalone.md)。 一般而言，我們建議您將 （獨立式） 並 （資料庫內） 安裝為互斥專為避免資源爭用，但如果您有足夠的資源有沒有 prohibitions 對兩者都安裝在同一部實體電腦上。

## <a name="choosing-between-in-database-and-standalone-analytics"></a>選擇資料庫中且獨立的分析

了解您的開發需求可協助您選擇 （資料庫） 和 （獨立式） 方法。 在獨立伺服器是容易設定和管理，如果您想要的最大的彈性，它使用的方式，或如果您想要連接至各種不同的 SQL Server 外部的資料來源。 

在資料庫內分析專為緊密結合的 SQL Server 中的資料。 您可以撰寫 T-SQL 查詢來呼叫 R 或 Python 函式，而執行 SQL Server Management Studio 或任何工具或應用程式用於外部或內嵌 T-SQL 指令碼。 如果您需要在執行 R 或 Python 程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，使用預存程序，或使用 SQL Server 執行個體做為[計算內容](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)，您必須安裝在資料庫內分析。 此選項提供最大的資料安全性以及與 SQL Server 工具整合。

同時在資料庫和獨立伺服器可以減輕開放原始碼 R 和 Python 的記憶體和處理條件約束。 這兩個選項會包含相同的套件和工具，能夠載入和處理大量資料上的多個核心，並彙總成單一的彙總輸出的結果。 函式和演算法設計成可調整和公用程式： 提供預測性分析、 統計模型、 資料視覺效果，與頂尖的機器學習服務演算法在商用伺服器產品中的設計和支援Microsoft。 

## <a name="components-of-an-in-database-installation"></a>在 資料庫安裝的元件

SQL Server 2016 只是 R。 SQL Server 2017 支援 R 和 Python。 下表描述每個版本的功能。 除了 SQL Server Launchpad 服務，此資料表是中所提供的相同[獨立 server 文章](r-server-standalone.md)。

| 元件 | 描述 |
|-----------|-------------|
| SQL Server Launchpad 服務 | 管理外部 R 和 Python 執行階段之間通訊的服務和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 |
| R 套件 | [RevoScaleR](revoscaler-overview.md)是可調整的 R，用於管理資料、 轉換、 visualzation，以及分析的函式與主要媒體櫃。  <br/>[MicrosoftML (R)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)新增機器學習演算法來建立自訂文字分析、 影像分析和情緒分析模型。 <br/>[mrsdeploy](operationalization-with-mrsdeploy.md)提供 web 服務部署 (SQL Server 2017 中只有）。 <br/>[olapR](how-to-create-mdx-queries-using-olapr.md)用於指定 MDX 查詢|
| Microsoft R Open (MRO) | [MRO](https://mran.microsoft.com/open)是 Microsoft 的開放原始碼散發套件的。會包含封裝和解譯器。 一律使用 MRO 配套在安裝程式中的版本。 |
| R 工具 | R 主控台視窗和命令提示字元是標準的工具，在 R 散發。 在 \Program files\Microsoft SQL Server\140\R_SERVER\bin\x64 中找到它們。 |
| R 範例和指令碼 |  開放原始碼 R 和 RevoScaleR 套件包含內建的資料集，讓您可以建立並使用預先安裝的資料執行指令碼。 在 \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets 和 \library\RevoScaleR 尋找它們。 |
| Python 套件 | [revoscalepy](../python/what-is-revoscalepy.md)是主要的程式庫適用於可調整的 Python 搭配資料操作、 轉換、 visualzation，和分析的函式。 <br/>[microsoftml (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)新增機器學習演算法來建立自訂文字分析、 影像分析和情緒分析模型。  |
| Python 工具 | 內建的 Python 命令列工具可用於臨機操作測試和工作項目。 在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe 中找到此工具。 |
| Anaconda | Anaconda 是開放原始碼散發套件的 Python 和基本封裝。 |
| Python 範例和指令碼 | 在使用 R、 Python 會包含內建的資料集與指令碼。 尋找 revoscalepy 資料在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site packages\revoscalepy\data\sample 資料。 |
| 預先定型的模型，在 R 和 Python | 預先定型的模型支援和可用的獨立伺服器上，但您無法透過 SQL Server 安裝程式來安裝它們。 安裝程式的 Microsoft Machine Learning 伺服器提供的模型，您可以安裝免費。 如需詳細資訊，請參閱 <<c0> [ 安裝預先定型的機器學習服務模型，在 SQL Server 上的](../install/sql-pretrained-models-install.md)。 |

## <a name="get-started-step-by-step"></a>開始逐步

啟動安裝程式、 將二進位檔附加至您最愛的開發工具和撰寫第一個指令碼。

### <a name="step-1-install-the-software"></a>步驟 1： 安裝軟體

安裝這些版本其中之一：

+ [SQL Server 2017 Machine Learning 服務 （資料庫）](../install/sql-machine-learning-services-windows-install.md)

+ [SQL Server 2016 R Services （資料庫內）-只有 R](../install/sql-r-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>步驟 2： 設定開發工具

設定您的開發工具，來使用 Machine Learning Server 二進位檔。 如需 Python 的詳細資訊，請參閱[連結 Python 二進位檔](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。 如需有關如何在 R Studio 中連接的指示，請參閱 <<c0> [ 使用不同版本的 R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R)指向 C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64 的工具。 您也可以試著[R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)。 

資料科學家通常使用 R 或 Python 自己的膝上型電腦或開發工作站上，瀏覽資料，以及建置和微調預測模型，直到達成良好的預測模型。 

使用 SQL Server 中的資料庫內分析，還有不需要變更此程序。 安裝完成後，您可以執行 R 或 Python 程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機或遠端：

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **使用您偏好的 IDE**。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 用戶端元件為資料科學家提供了所有進行實驗與開發所需的工具。 這些工具包括 R 執行階段 (大幅提升標準 R 作業效能的 Intel 核心數學程式庫)，以及一組支援在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中執行 R 程式碼的增強型 R 套件。  

+ **使用遠端或本機**。 資料科學家可以連線至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，一如往常將資料帶入用戶端進行本機分析。 不過，較好的解決方案是使用**RevoScaleR**或是**revoscalepy** Api 將計算推送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦，避免成本高同時不安全的資料移動。

+ **內嵌中的 R 或 Python 指令碼[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序**。 當您的程式碼完全最佳化時，請將它包裝在預存程序中，以避免不必要的資料移動，並最佳化資料處理工作。

### <a name="step-3-write-your-first-script"></a>步驟 3： 撰寫您的第一個指令碼

呼叫 R 或 Python 函式從 T-SQL 指令碼內：
  
  + [R：在 Transact-SQL 中使用 R 程式碼](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md) 
  + [R：適用於 SQL 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)
  + [Python：使用 T-SQL 執行 Python](../tutorials/run-python-using-t-sql.md)
  + [Python：適用於 SQL 開發人員的資料庫內分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

選擇工作的最佳語言。 R 是最適合使用 SQL 實作困難的統計計算。 資料的集合式作業，利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以達到最大效能。 使用記憶體中資料庫引擎進行非常快速的計算資料行。

### <a name="step-4-optimize-your-solution"></a>步驟 4： 最佳化您的解決方案

備妥可調整的企業資料模型時，資料科學家通常適用於 DBA 或 SQL 開發人員最佳化程序，例如︰

+ 特徵工程
+ 資料擷取和資料轉換
+ 計分

傳統上使用 R 的資料科學家有問題的效能和延展性，尤其是使用大型資料集。 這是因為通用執行階段實作是單一執行緒，而且可以容納放入本機電腦上的可用記憶體的資料集。 與 SQl Server Machine Learning 服務整合會提供多項功能，以提升效能、 更多資料：

+ **RevoScaleR**： 此 R 封裝包含一些最受歡迎的 R 函數，經過重新設計可提供平行處理與延展的實作。 此套件包含能進一步提升效能與延展性的函數，方法是將計算推送至通常記憶體較大且運算能力更佳的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。

+ **revoscalepy**。 此 Python 程式庫，可以在 SQL Server 2017 中，使用遠端計算內容，例如 RevoScaleR 中, 實作最受歡迎的函式和許多支援的演算法分散式處理。

**資源**

+ [效能案例研究](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R 和資料最佳化](../../advanced-analytics/r/r-and-data-optimization-r-services.md)

### <a name="step-5-deploy-and-consume"></a>步驟 5： 部署和取用

指令碼或模型可供生產環境使用之後，資料庫開發人員可能會嵌入程式碼或模型預存程序中，以便可以從應用程式呼叫的已儲存的 R 或 Python 程式碼。 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 儲存及執行 R 程式碼有許多優點︰您可以使用方便的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 介面和所有發生在資料庫中的計算，避免不必要的資料移動。

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **安全且可擴充**。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用新的擴充性架構，保持您資料庫引擎的安全，並隔離 R 和 Python 的工作階段。 您也可以控制可以執行指令碼的使用者，您可以指定可以存取的程式碼的資料庫。 您可以控制配置給執行階段，以避免大量計算危及整體伺服器效能的資源數量。

+ **排程和稽核**。 執行外部指令碼工作時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以控制和資料科學家所使用的稽核資料。 您也可以排定工作並撰寫包含外部的 R 或 Python 指令碼，就像任何其他的 T-SQL 作業或預存程序，您會排程工作流程。

若要充分利用的資源管理和安全性功能在 SQL Server 中，部署程序可能會包含這些工作：

+ 將 yourcode 轉換成可以在預存程序中以最佳方式執行的函式
+ 設定安全性和鎖定在特定工作所使用的套件
+ 啟用資源控管 （需要 Enterprise edition）

**資源**

+ [適用於 R 的資源控管](resource-governance-for-r-services.md)
+ [SQL Server 的 R 封裝管理](install-additional-r-packages-on-sql-server.md)

## <a name="see-also"></a>另請參閱

 [SQL Server Machine Learning 及 R Server （獨立式）](sql-server-r-services.md)
