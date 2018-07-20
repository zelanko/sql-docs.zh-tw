---
title: SQL Server Machine Learning 伺服器 （獨立式） 和 R Server （獨立式） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a8cdceabc26c55b6eade57712fa610d3e84808f5
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174785"
---
# <a name="sql-server-machine-learning-server-standalone-and-r-server-standalone"></a>SQL Server Machine Learning 伺服器 （獨立式） 和 R Server （獨立式）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在獨立伺服器是安裝的機器學習服務元件，categories-<objectid> 的 R 和 Python，獨立 SQL Server database engine 執行個體執行的功能。 您可以安裝在獨立伺服器本身，不含 SQL Server 上的相依性。 因為在獨立伺服器都是獨立的 SQL Server、 設定和管理工作和工具，更類似於非 SQL 版本的 Machine Learning 伺服器，您可以在閱讀[這篇文章](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。

Server 獨立機器學習的目的是要提供豐富的開發環境，與針對小型到大型資料集，使用專屬的套件和計算引擎的 R 和 Python 工作負載的分散式和平行處理與伺服器一起安裝。 在獨立伺服器上的 R 和 Python 套件會提供在 SQL Server （資料庫） 安裝中，允許程式碼可攜性相同並[計算內容切換](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。

主要原因開發人員會選擇獨立 machine learning 伺服器是超越開放原始碼 R 和 Python 的記憶體和處理條件約束。 獨立伺服器可以載入並處理對多個核心大量的資料和彙總成單一的彙總輸出的結果。 函式和演算法設計成可調整和公用程式： 提供預測性分析、 統計模型、 資料視覺效果，與頂尖的機器學習服務演算法在商用伺服器產品中的設計和支援Microsoft。

一般而言，我們建議您將 （獨立式） 並 （資料庫內） 安裝為互斥 exclusive 避免資源爭用，但如果您有足夠的資源，沒有任何禁止對兩者都安裝在同一部實體電腦上。

您的電腦上只能有一部獨立伺服器： 任一[SQL Server 2017 Machine Learning Server （獨立式）](../install/sql-machine-learning-standalone-windows-install.md)或是[SQL Server 2016 R Server （獨立式）](../install/sql-r-standalone-windows-install.md)。 您必須手動安裝不同版本之前解除安裝一個版本。

## <a name="components-of-a-standalone-server"></a>獨立伺服器的元件

SQL Server 2016 只是 R。 SQL Server 2017 支援 R 和 Python。 下表描述每個版本的功能。

| 元件 | 描述 |
|-----------|-------------|
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

+ [SQL Server 2017 Machine Learning Server （獨立式）](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server （獨立式）-只有 R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>步驟 2： 設定開發工具

設定您的開發工具，來使用 Machine Learning Server 二進位檔。 如需 Python 的詳細資訊，請參閱[連結 Python 二進位檔](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。 如需有關如何在 R Studio 中連接的指示，請參閱 <<c0> [ 使用不同版本的 R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R)指向 C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64 的工具。 您也可以試著[R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)。 

### <a name="step-3-write-your-first-script"></a>步驟 3： 撰寫您的第一個指令碼

撰寫使用來自 RevoScaleR、 revoscalepy 和機器學習演算法的函式中的 R 或 Python 指令碼。
  
  + [探索 R 和 25 個函數中的 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)： 開始使用 R 的基本命令，然後進行 RevoScaleR 可散布分析函數，提供高效能和調整 R 解決方案。 包含許多最熱門 R 模型建立套件 (例如 	K-Means 叢集、決策樹及決策樹系) 的可平行處理版本，以及資料操作工具。

  + [快速入門： 使用 microsoftml Python 套件的二進位分類的範例](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml)： 建立使用 microsoftml 與已知乳癌特徵資料集的函式的二元分類模型。

選擇工作的最佳語言。 R 是最適合使用 SQL 實作困難的統計計算。 資料的集合式作業，利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以達到最大效能。 使用記憶體中資料庫引擎進行非常快速的計算資料行。

### <a name="step-4-operationalize-your-solution"></a>步驟 4： 操作您的解決方案

獨立伺服器可以使用[operationalization](https://docs.microsoft.com//machine-learning-server/what-is-operationalization)功能的非 SQL-品牌[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。 您可以設定獨立的伺服器進行運作，提供下列優點： 部署和裝載您的程式碼，因為 web 服務、 執行診斷，測試 web 服務的容量。

## <a name="see-also"></a>另請參閱

 [SQL Server Machine Learning 服務 （資料庫）](sql-server-r-services.md)

