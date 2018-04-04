---
title: "SQL Server 機器學習伺服器 （獨立） 與 R Server （獨立） |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
vms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: eb30dbfdfd03f5a6515d0559d7f60cdde7b9223c
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2018
---
# <a name="sql-server-machine-learning-server-standalone-and-r-server-standalone"></a>SQL Server 機器學習伺服器 （獨立） 與 R Server （獨立）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在獨立伺服器是安裝的機器學習元件，以做為 R，並將 Python，獨立 SQL Server database engine 執行個體執行的功能。 您可以安裝在獨立伺服器本身，與 SQL Server 上沒有相依性。 因為在獨立伺服器都是獨立的 SQL Server、 設定和管理工作和工具是比較類似於非 SQL 版本的機器學習伺服器，您可以在閱讀[本文](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。

獨立的機器學習服務伺服器的目標是提供豐富的開發環境，與 R，並將 Python 針對小型到大型資料集，使用專用的封裝和計算引擎的工作負載的分散式和平行處理與伺服器一起安裝。 獨立伺服器上的 R 和 Python 封裝是安裝 SQL Server （資料庫），允許程式碼可攜性中所提供相同和[計算內容切換](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。

主要原因開發人員選擇獨立機器學習伺服器是超越開放原始碼 R 和 Python 的記憶體和處理條件約束。 獨立伺服器可以載入和處理多個核心上大量的資料和彙總成單一的彙總輸出的結果。 函式和演算法針對標尺和公用程式所設計： 提供的預測分析、 建立統計模型、 資料視覺化，以及先進機器學習演算法商業伺服器產品中的工程和支援Microsoft。

一般而言，我們建議您將 （獨立） 並 （資料庫） 安裝為互斥獨佔避免資源爭用，但如果您有足夠的資源沒有針對它們兩個安裝在同一部實體電腦上沒有禁止。

您的電腦上只能有一部獨立伺服器： 任一[SQL Server 2017 機器學習伺服器 （獨立）](../install/sql-machine-learning-standalone-windows-install.md)或[SQL Server 2016 R 伺服器 （獨立）](../install/sql-r-standalone-windows-install.md)。 您必須手動安裝不同版本之前解除安裝版本。

## <a name="components-of-a-standalone-server"></a>獨立伺服器的元件

SQL Server 2016 只是 R。 SQL Server 2017 支援 R 和 Python。 下表描述每個版本的功能。

| 元件 | Description |
|-----------|-------------|
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

+ [SQL Server 2017 機器學習伺服器 （獨立）](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R 伺服器 （獨立）-只有 R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>步驟 2： 設定開發工具

設定您的開發工具，若要使用的機器學習伺服器二進位檔。 如需 Python 的詳細資訊，請參閱[連結 Python 二進位檔](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。 如需有關如何在 R Studio 中連接的指示，請參閱[使用不同版本的 R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R)點指派到 C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64 工具。 您也可以嘗試[R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)。 

### <a name="step-3-write-your-first-script"></a>步驟 3： 撰寫第一個指令碼

撰寫從 RevoScaleR、 revoscalepy 和機器學習演算法的函式的使用中的 R 或 Python 指令碼。
  
  + [R 與 RevoScaleR 25 函式中的，瀏覽](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)： 開頭為基本的 R 命令，然後 RevoScaleR 可散布分析函式可提供高效能的進度和縮放 R 解決方案。 包含許多最熱門 R 模型建立套件 (例如 	K-Means 叢集、決策樹及決策樹系) 的可平行處理版本，以及資料操作工具。

  + [快速入門： 的 microsoftml Python 封裝的二進位分類範例](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml)： 建立二元分類模型使用從 microsoftml 和已知乳癌 cancer 資料集的函式。

選擇工作的最佳語言。 R 最適用於統計計算很難使用 SQL 實作。 透過資料的集合式作業，利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]達到最佳效能。 使用記憶體中資料庫引擎非常快速的計算資料行。

### <a name="step-4-operationalize-your-solution"></a>步驟 4： 推動您的方案

獨立伺服器可使用[實施](https://docs.microsoft.com//machine-learning-server/what-is-operationalization)功能的非 SQL-品牌[Microsoft Machine Learning 伺服器](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。 您可以設定的獨立伺服器實施，它將提供這些優點： 部署和執行診斷的 web 服務測試 web 服務的容量時，裝載您的程式碼。

## <a name="see-also"></a>另請參閱

 [SQL Server 機器學習服務 （資料庫）](sql-server-r-services.md)

