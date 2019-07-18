---
title: 獨立式 R Server 或 Machine Learning 伺服器安裝-SQL Server Machine Learning 服務
description: 概觀簡介獨立的 R Server 和 SQL Server 安裝程式中的 Machine Learning Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: overview
author: dphansen
ms.author: davidph
ms.openlocfilehash: 407a4c87101b2d422afbb982c7a07d92e84d26f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962515"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>R Server （獨立式） 和 SQL Server 中的 Machine Learning Server （獨立式）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 提供獨立的 R Server 或 SQL Server 獨立執行的 Machine Learning 伺服器安裝支援。 根據您的 SQL Server 版本，在獨立伺服器具有開放原始碼 R 和可能是 Python，重疊在擴展加入統計和預測性分析來自 Microsoft 的高效能程式庫的基礎。 程式庫也可讓以 R 或 Python 指令碼的機器學習工作。 

在 SQL Server 2016 中，這項功能稱為**R Server （獨立式）** ，且僅限 R。 在 SQL Server 2017 中，它會呼叫**Machine Learning Server （獨立式）** ，其中包括 R 和 Python。  

> [!Note]
> 安裝 SQL Server 安裝程式，在獨立伺服器功能上相當於非 SQL 品牌版本[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，支援相同的使用者情節，包括遠端執行，運算化和 web 服務，以及一組完整的 R 和 Python 程式庫。

## <a name="components"></a>元件

SQL Server 2016 只是 R。 SQL Server 2017 支援 R 和 Python。 下表描述每個版本的功能。

| 元件 | 描述 |
|-----------|-------------|
| R 套件 | [**RevoScaleR** ](ref-r-revoscaler.md)可調整的 R 與資料操作、 轉換、 視覺化和分析的函式中為主要媒體櫃。  <br/>[**MicrosoftML** ](ref-r-microsoftml.md)新增機器學習演算法來建立自訂文字分析、 影像分析和情緒分析模型。 <br/>[**sqlRUtils** ](ref-r-sqlrutils.md)提供 helper 函式將 R 指令碼放入 T-SQL 預存程序、 註冊預存程序使用資料庫時，以及從 R 開發環境執行預存程序。<br/>[**mrsdeploy** ](operationalization-with-mrsdeploy.md)提供 web 服務部署 (SQL Server 2017 中只有）。 <br/>[**olapR** ](ref-r-olapr.md)用於指定 MDX 查詢|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open)是 Microsoft 的開放原始碼散發套件的。會包含封裝和解譯器。 一律使用 MRO 配套在安裝程式中的版本。 |
| R 工具 | R 主控台視窗和命令提示字元是標準的工具，在 R 散發。 在 \Program files\Microsoft SQL Server\140\R_SERVER\bin\x64 中找到它們。 |
| R 範例和指令碼 |  開放原始碼 R 和 RevoScaleR 套件包含內建的資料集，讓您可以建立並使用預先安裝的資料執行指令碼。 在 \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets 和 \library\RevoScaleR 尋找它們。 |
| Python 套件 | [**revoscalepy** ](../python/ref-py-revoscalepy.md)是主要的程式庫適用於可調整的 Python 搭配資料操作、 轉換、 視覺效果和分析的函式。 <br/>[**microsoftml** ](../python/ref-py-microsoftml.md)新增機器學習演算法來建立自訂文字分析、 影像分析和情緒分析模型。  |
| Python 工具 | 內建的 Python 命令列工具可用於臨機操作測試和工作項目。 在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe 中找到此工具。 |
| Anaconda | Anaconda 是開放原始碼散發套件的 Python 和基本封裝。 |
| Python 範例和指令碼 | 在使用 R、 Python 會包含內建的資料集與指令碼。 尋找 revoscalepy 資料在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site packages\revoscalepy\data\sample 資料。 |
| 預先定型的模型，在 R 和 Python | 預先定型的模型建立的特定使用案例，並由 Microsoft 的資料科學工程小組所維護。 您可以使用預先定型的模型，以-為評分正負面情感的文字，或在映像，使用您提供的新資料輸入中偵測功能。 預先定型的模型支援和可用的獨立伺服器上，但您無法透過 SQL Server 安裝程式來安裝它們。 如需詳細資訊，請參閱 <<c0> [ 安裝預先定型的機器學習服務模型，在 SQL Server 上的](../install/sql-pretrained-models-install.md)。 |

## <a name="using-a-standalone-server"></a>使用獨立伺服器

R 和 Python 開發人員通常會選擇獨立伺服器，以超越開放原始碼 R 和 Python 的記憶體和處理條件約束。 在獨立伺服器上執行的 R 和 Python 程式庫可以載入並處理多個核心上大量的資料和彙總成單一的彙總輸出的結果。 高效能函數設計成可調整和公用程式： 提供預測性分析、 統計模型、 資料視覺效果，與頂尖的機器學習服務演算法在商用伺服器產品中的設計和支援Microsoft。

與 SQL Server 分離的獨立伺服器，為 R 和 Python 環境設定的安全，並使用基礎作業系統和獨立伺服器，而不是 SQL Server 中提供的標準工具存取。 沒有內建支援的 SQL Server 關聯式資料。 如果您想要使用 SQL Server 資料，您可以建立資料來源物件和連線，如同從任何用戶端。

作為 SQL Server 的輔助，獨立伺服器也很有用做為功能強大的開發環境如果您需要本機和遠端運算。 在獨立伺服器上的 R 和 Python 套件會與所提供以程式碼可攜性的資料庫引擎安裝相同並[計算內容切換](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。

## <a name="how-to-get-started"></a>如何開始使用

啟動安裝程式、 將二進位檔附加至您最愛的開發工具和撰寫第一個指令碼。

### <a name="step-1-install-the-software"></a>步驟 1：安裝軟體

安裝這些版本其中之一：

+ [SQL Server 2017 Machine Learning Server （獨立式）](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server （獨立式）-只有 R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>步驟 2：設定開發工具

在獨立伺服器上，通常會在本機上使用安裝在同一部電腦上的開發工作。

+ [設定 R 工具](set-up-a-data-science-client.md)
+ [設定 Python 工具](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>步驟 3：撰寫第一個指令碼

撰寫使用來自 RevoScaleR、 revoscalepy 和機器學習演算法的函式中的 R 或 Python 指令碼。
  
  + [探索 R 和 25 個函數中的 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler):開始使用 R 的基本命令，再進展到 RevoScaleR 可散布分析函數，提供高效能和調整 R 解決方案。 包含許多最熱門 R 模型建立套件 (例如 	K-Means 叢集、決策樹及決策樹系) 的可平行處理版本，以及資料操作工具。

  + [快速入門：使用 microsoftml Python 套件的二進位分類範例](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml):建立使用 microsoftml 與已知乳癌特徵資料集的函式的二元分類模型。

選擇工作的最佳語言。 R 是最適合使用 SQL 實作困難的統計計算。 資料的集合式作業，利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以達到最大效能。 使用記憶體中資料庫引擎進行非常快速的計算資料行。

### <a name="step-4-operationalize-your-solution"></a>步驟 4：操作您的方案

獨立伺服器可以使用[operationalization](https://docs.microsoft.com//machine-learning-server/what-is-operationalization)功能的非 SQL-品牌[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。 您可以設定獨立的伺服器進行運作，提供下列優點： 部署和裝載您的程式碼，因為 web 服務、 執行診斷，測試 web 服務的容量。

### <a name="step-5-maintain-your-server"></a>步驟 5：維護您的伺服器

SQL Server 版本上定期執行的累計更新。 套用累計更新將安全性和功能的增強功能加入至現有安裝。 

描述新的或已變更的功能可以中找到[CAB 下載](../install/sql-ml-cab-downloads.md)文章和為網頁上[SQL Server 2016 累積更新](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions)和[SQL Server 2017 累積更新](https://support.microsoft.com/help/4047329). 

如需有關如何將更新套用至現有的執行個體的詳細資訊，請參閱 <<c0> [ 套用更新](../install/sql-machine-learning-standalone-windows-install.md#apply-cu)中的安裝指示。

## <a name="see-also"></a>另請參閱

 [安裝 R Server （獨立式） 或 Machine Learning 伺服器 （獨立式）](../install/sql-machine-learning-standalone-windows-install.md)

