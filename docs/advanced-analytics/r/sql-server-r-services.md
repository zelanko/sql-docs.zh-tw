---
title: SQL Server 機器學習和 R 服務 （資料庫） |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 559309a29944f20f8c006ccc92769f0b2824e3b3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585960"
---
# <a name="sql-server-machine-learning-and-r-services-in-database"></a>SQL Server 機器學習和 R 服務 （資料庫）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

機器學習的資料庫中安裝 SQL Server 資料庫引擎執行個體，提供 SQL Server 執行個體中的內建資料的 R，並將 Python 外部指令碼支援的內容中的運作方式。 因為與整合在機器學習[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以讓分析資料並不需要成本和移動資料相關聯的安全性風險。

因為 database engine 是多重執行個體，您可以安裝多個執行個體或甚至較舊的資料庫中分析和較新版本的並存。 選擇包含[SQL Server 2017 機器學習服務 （資料庫）](../install/sql-machine-learning-standalone-windows-install.md)與 R 和 Python 或[SQL Server 2016 R 服務 （資料庫）](../install/sql-r-standalone-windows-install.md)與剛。 

機器學習元件也可以安裝為無從驗證執行個體的[獨立伺服器](r-server-standalone.md)。 一般而言，我們建議您將 （獨立） 並 （資料庫） 安裝為互斥獨佔避免資源爭用，但如果您有足夠的資源有沒有 prohibitions 針對它們兩個安裝在同一部實體電腦上。

## <a name="choosing-between-in-database-and-standalone-analytics"></a>在資料庫和獨立分析之間選擇

了解您的開發需求可協助您選擇 （資料庫） 和 （獨立） 方法。 容易設定和管理，如果您想要它使用的方式相當大的彈性，或如果您想要也連接到各種不同的 SQL Server 外部資料來源是獨立伺服器。 

在資料庫分析專為 SQL Server 中的資料與深度整合。 您可以撰寫呼叫 R 或 Python 函式和 SQL Server Management Studio 或任何工具或使用外部或內嵌 t-sql 應用程式中執行指令碼的 T-SQL 查詢。 如果您需要執行中 R 或 Python 程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，使用預存程序，或使用 SQL Server 執行個體做為[計算內容](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)，您必須安裝在資料庫分析。 此選項提供最大資料安全性和 SQL Server 工具與整合。

同時在資料庫和獨立伺服器可以減輕的開放原始碼 R 和 Python 的記憶體和處理條件約束。 這兩個選項會包含相同的封裝和工具，能夠載入和處理多個核心上大量的資料和彙總成單一的彙總輸出的結果。 函式和演算法針對標尺和公用程式所設計： 提供的預測分析、 建立統計模型、 資料視覺化，以及先進機器學習演算法商業伺服器產品中的工程和支援Microsoft。 

## <a name="components-of-an-in-database-installation"></a>在 資料庫安裝的元件

SQL Server 2016 只是 R。 SQL Server 2017 支援 R 和 Python。 下表描述每個版本的功能。 除了 SQL Server Launchpad 服務，此資料表是與所提供的相同[獨立 server 文章](r-server-standalone.md)。

| 元件 | 描述 |
|-----------|-------------|
| SQL Server Launchpad 服務 | 管理外部 R，並將 Python 執行階段之間通訊的服務和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 |
| R 封裝 | [RevoScaleR](revoscaler-overview.md)搭配資料操作、 轉換、 visualzation，和分析的函式的可延展為主要媒體櫃。  <br/>[MicrosoftML (R)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)新增機器學習演算法，來建立自訂文字分析、 影像分析和情緒分析模型。 <br/>[mrsdeploy](operationalization-with-mrsdeploy.md)提供 web 服務部署 （在 SQL Server 2017 只)。 <br/>[olapR](how-to-create-mdx-queries-using-olapr.md)適用於在 r 中指定的 MDX 查詢|
| Microsoft R Open (MRO) | [MRO](https://mran.microsoft.com/open)是 Microsoft 的開放原始碼分佈是。封裝和解譯器都會加入。 一律使用 MRO 配套在安裝程式中的版本。 |
| R 工具 | R 主控台視窗和命令提示字元會在 R 散發的標準工具。 在 SQL Server\140\R_SERVER\bin\x64 \Program files\Microsoft 中找到它們。 |
| R 範例和指令碼 |  開放原始碼 R 與 RevoScaleR 封裝包含內建的資料集，因此您可以建立並使用預先安裝的資料執行指令碼。 在 \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets 和 \library\RevoScaleR 尋找它們。 |
| Python 封裝 | [revoscalepy](../python/what-is-revoscalepy.md)搭配資料操作、 轉換、 visualzation，和分析的函式的可延展 python 為主要媒體櫃。 <br/>[microsoftml (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)新增機器學習演算法，來建立自訂文字分析、 影像分析和情緒分析模型。  |
| Python 工具 | 內建的 Python 命令列工具可用於臨機操作測試和工作項目。 在 SQL Server\140\PYTHON_SERVER\python.exe \Program files\Microsoft 尋找工具。 |
| Anaconda | Anaconda 是開放原始碼分佈的 Python 和基本封裝。 |
| Python 範例和指令碼 | 如同 R、 Python 包含內建的資料集和指令碼。 在 SQL \Program files\Microsoft 尋找 revoscalepy 資料 Server\140\PYTHON_SERVER\lib\site packages\revoscalepy\data\sample 資料。 |
| 在 R 和 Python 中預先定型的模型 | 預先定型的模型支援並可在獨立伺服器上，但您無法透過 SQL Server 安裝程式安裝它們。 Microsoft Machine Learning 伺服器的安裝程式提供模型中，您可以安裝免費。 如需詳細資訊，請參閱[安裝預先定型的 SQL Server 上的機器學習模型](install-pretrained-models-sql-server.md)。 |

## <a name="get-started-step-by-step"></a>開始逐步

啟動安裝程式，將二進位檔附加至您最愛的開發工具，並撰寫第一個指令碼。

### <a name="step-1-install-the-software"></a>步驟 1： 安裝軟體

安裝這些版本其中一個：

+ [SQL Server 2017 機器學習服務 （資料庫）](../install/sql-machine-learning-services-windows-install.md)

+ [SQL Server 2016 R 服務 （資料庫）-只有 R](../install/sql-r-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>步驟 2： 設定開發工具

設定您的開發工具，若要使用的機器學習伺服器二進位檔。 如需 Python 的詳細資訊，請參閱[連結 Python 二進位檔](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。 如需有關如何在 R Studio 中連接的指示，請參閱[使用不同版本的 R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R)點指派到 C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64 工具。 您也可以嘗試[R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)。 

資料科學家通常使用 R 或 Python 自己膝上型電腦或開發工作站上，瀏覽資料，並建置並微調預測模型，直到達成良好的預測模型為止。 

資料庫在分析 SQL Server 中，沒有需要變更此程序。 安裝完成之後，您可以執行 R 或 Python 程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機或遠端方式：

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **使用您偏好的 IDE**。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 用戶端元件為資料科學家提供了所有進行實驗與開發所需的工具。 這些工具包括 R 執行階段 (大幅提升標準 R 作業效能的 Intel 核心數學程式庫)，以及一組支援在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中執行 R 程式碼的增強型 R 套件。  

+ **使用遠端或本機**。 資料科學家可以連線至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，一如往常將資料帶入用戶端進行本機分析。 不過，較好的解決方案是使用**RevoScaleR**或**revoscalepy** Api 將計算推送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦，避免成本高同時不安全的資料移動。

+ **內嵌 R 或 Python 指令碼中的[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序**。 當您的程式碼已完整最佳化時，將其包裝在預存程序中，可以避免不必要的資料移動，並最佳化資料處理工作。

### <a name="step-3-write-your-first-script"></a>步驟 3： 撰寫第一個指令碼

呼叫 R 或 Python 從函式內 T-SQL 指令碼：
  
  + [R：在 Transact-SQL 中使用 R 程式碼](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md) 
  + [R：適用於 SQL 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)
  + [Python：使用 T-SQL 執行 Python](../tutorials/run-python-using-t-sql.md)
  + [Python：適用於 SQL 開發人員的資料庫內分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

選擇工作的最佳語言。 R 最適用於統計計算很難使用 SQL 實作。 透過資料的集合式作業，利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]達到最佳效能。 使用記憶體中資料庫引擎非常快速的計算資料行。

### <a name="step-4-optimize-your-solution"></a>步驟 4： 最佳化您的方案

模型上的企業資料縮放就緒時，資料科學家通常運作方式與 DBA 或 SQL 開發人員最佳化程序，例如：

+ 特徵工程
+ 擷取資料和資料轉換
+ 計分

傳統上使用 R 的資料科學家會有問題的效能和延展性，尤其是使用大型資料集。 這是因為通用執行階段實作是單一執行緒，而且可以容納放入本機電腦上的可用記憶體的資料集。 與 SQl Server 機器學習服務整合提供多項功能，以提升效能、 更多資料：

+ **RevoScaleR**： 此 R 封裝包含某些熱門 R 函數，經過重新設計可提供平行處理原則與規模的實作。 此套件包含能進一步提升效能與延展性的函數，方法是將計算推送至通常記憶體較大且運算能力更佳的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。

+ **revoscalepy**。 此 Python 程式庫，提供 SQL Server 2017，實作 RevoScaleR 中, 最受歡迎的函式，例如遠端計算內容和許多支援的演算法分散式處理。

**資源**

+ [效能案例研究](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R 和資料最佳化](../../advanced-analytics/r/r-and-data-optimization-r-services.md)

### <a name="step-5-deploy-and-consume"></a>步驟 5： 部署和使用

指令碼或模型可供生產環境使用之後，資料庫開發人員可能會內嵌程式碼或模型預存程序，以便儲存的 R 或 Python 程式碼可以呼叫的應用程式。 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 儲存及執行 R 程式碼有許多優點︰您可以使用方便的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 介面和所有發生在資料庫中的計算，避免不必要的資料移動。

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **安全且可延伸**。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用新的擴充性架構，保持您資料庫引擎的安全，並隔離開 R，並將 Python 的工作階段。 您也可以控制使用者可以執行指令碼，以及您可以指定可以存取的程式碼的資料庫。 您可以控制配置給執行階段，以防止從大量計算危及整體伺服器效能的資源數量。

+ **排程和稽核**。 執行外部指令碼工作時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 您可以控制和稽核資料供資料科學家。 您也可以排定工作並撰寫包含外部的 R 或 Python 指令碼，就像任何其他 T-SQL 作業或預存程序，您會排程工作流程。

若要充分利用的資源管理和安全性功能在 SQL Server 中，部署程序可能包括下列工作：

+ 將 yourcode 轉換成可以在預存程序中以最佳方式執行的函式
+ 設定安全性，以及鎖定特定的工作所使用的封裝
+ 啟用資源監管 （需要 Enterprise edition）

**資源**

+ [資源管理針對 R](resource-governance-for-r-services.md)
+ [SQL Server 的 R 封裝管理](install-additional-r-packages-on-sql-server.md)

## <a name="see-also"></a>另請參閱

 [SQL Server 機器學習和 R 伺服器 （獨立）](sql-server-r-services.md)
