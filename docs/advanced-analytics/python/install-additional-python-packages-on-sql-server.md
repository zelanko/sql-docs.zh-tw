---
title: "SQL Server 上安裝新的 Python 封裝 |Microsoft 文件"
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 78a76403f3212c7619afbf02577075161699fbd6
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="install-new-python-packages-on-sql-server"></a>SQL Server 上安裝新的 Python 封裝

本文說明如何在 SQL Server 2017 的執行個體上安裝新的 Python 封裝。

它也會描述如何列出已安裝在目前的環境中的封裝。

## <a name="prerequisites"></a>Prerequisites

安裝新套件的程序非常類似的標準的 Python 環境中。 不過，一些額外的步驟所需，如果伺服器沒有網際網路連線。

+ 您必須安裝機器學習服務 （資料庫） 與 Python 語言選項。 如需指示，請參閱[Python 機器學習服務設定](setup-python-machine-learning-services.md)。

+ 每個伺服器執行個體中，您必須安裝個別封裝的副本。 封裝無法執行個體之間共用。

+ 決定使用 Python 3.5 和 Windows 環境中，您想要使用的封裝是否會運作。 

    一般情況下，有幾項限制，您可以匯入，並在 SQL Server 環境中使用的封裝。 可能的問題包括具有無法在 Windows 電腦安裝的相依性或在伺服器或防火牆，使用已封鎖的網路功能的封裝。

+ 伺服器的系統管理權限才能安裝封裝。

## <a name="add-a-new-python-package"></a>加入新的 Python 封裝

此範例中，我們假設您想要直接在 SQL Server 電腦上安裝新的封裝。

在此範例中所安裝的套件[CNTK](https://docs.microsoft.com/cognitive-toolkit/)，深入學習 microsoft 的支援自訂，定型集，和不同類型的類神經網路共用的架構。

> [!TIP]
> 需要設定您的 Python 工具的說明？ 請參閱這些部落格：
> 
> [開始使用 Python Web 服務使用機器學習伺服器](https://blogs.msdn.microsoft.com/mlserver/2017/12/13/getting-started-with-python-web-services-using-machine-learning-server/)
> 
> [David 臂： Microsoft 認知 Toolkit + VS 程式碼](http://dacrook.com/cntk-vs-code-awesome/)

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>步驟 1： 下載了 Python 封裝的 Windows 版本

+ 如果您沒有網際網路存取的伺服器上安裝 Python 封裝，您必須 WHL 檔案下載到另一部電腦，並將它複製到伺服器。

    例如，在個別電腦上，您可以下載 WHL 檔案從這個站台[https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)，然後將檔案複製`cntk-2.1-cp35-cp35m-win_amd64.whl`到 SQL Server 電腦上的本機資料夾。

+ SQL Server 2017 使用 Python 3.5。 請務必取得封裝的 Windows 版本和 Python 3.5 與相容的版本。

此頁面包含多個平台與多個的 Python 版本的下載：[設定 CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>步驟 2： 開啟 Python 命令提示字元

找出 SQL Server 所使用的預設 Python 程式庫位置。 如果您已安裝多個執行個體，請務必找出您要加入封裝的執行個體的 PYTHON_SERVICE 資料夾。

例如，如果機器學習服務已安裝，使用預設值，和機器學習服務已啟用預設執行個體上，路徑會，如下所示：

    `C:\Program Files\Microsoft SQL  Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

開啟 Python 命令提示字元中執行個體相關聯。

> [!TIP]
> 我們建議您設定的 Python 環境特有的機器學習 Server 或 SQL Server。

### <a name="step-3-install-the-package-using-pip"></a>步驟 3： 使用 pip 安裝套件

+ 如果您習慣使用 Python 命令列，使用 PIP.exe 來安裝新的封裝。 您可以找到**pip**安裝程式中的`Scripts`子資料夾。 

    如果您收到錯誤， **pip**無法辨識為內部或外部命令，您可以加入的 PATH 變數中 Windows 的 Python 可執行檔和 Python 指令碼資料夾的路徑。

    完整路徑**指令碼**預設安裝中的資料夾如下所示：

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts`

+ 如果您正在使用 Visual Studio 2017 或 Visual Studio 2015 的 Python 擴充功能，您可以執行`pip install`從**Python 環境**視窗。 按一下**封裝**，並在文字方塊中，提供的名稱或要安裝之封裝的位置。 您不需要輸入`pip install`; 它會為您自動填入。 

    - 如果電腦沒有網際網路存取，請提供封裝的名稱或為特定套件和版本的 URL。 例如，若要安裝的版本支援適用於 Windows 和 Python 3.5 CNTK，您可以指定的下載 URL:`https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - 如果電腦沒有網際網路存取，您應該已經下載 WHL 檔案事先。 然後，指定的本機檔案路徑和名稱。 例如，貼上的下列路徑和檔案，以安裝從網站下載的 WHL 檔案：`"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

您可能會提示您提升權限來完成安裝。

安裝進度，您可以看到在 [命令提示字元] 視窗的狀態訊息：

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```



### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>步驟 4： 載入封裝或其函式做為您的指令碼的一部分

安裝完成時，您可以立即開始使用封裝中的下一個步驟所述。

使用 CNTK，深入學習範例，請參閱這些教學課程： [CNTK API Python](https://cntk.ai/pythondocs/tutorials.html)

若要使用封裝中的函式指令碼中，插入標準`import <package_name>`初始行指令碼中的陳述式：

```python
import numpy as np
import cntk as cntk
cntk._version_
```

##  <a name="how-to-view-installed-packages-using-conda"></a>如何檢視已安裝的封裝使用 conda

有不同的方式，您可以取得已安裝的封裝清單。 例如，您可以檢視已安裝的封裝中**Python 環境**的 Visual Studio 視窗。

如果您使用 Python 命令列，您可以使用**conda**封裝管理員，就會包含與 SQL Server 安裝程式新增 Anaconda Python 環境。

若要檢視已安裝目前的環境中的 Python 封裝，請從命令提示字元視窗執行此命令：

```python
conda list
```

如需有關**conda**以及如何使用它來建立和管理多個 Python 環境，請參閱[管理環境與 conda](https://conda.io/docs/user-guide/tasks/manage-environments.html)。
