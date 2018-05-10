---
title: 在 SQL Server 機器學習上安裝新的 Python 封裝 |Microsoft 文件
description: 將新的 Python 封裝加入至 SQL Server 2017 機器學習服務 （資料庫） 和機器學習伺服器 （獨立）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2db7792c8c7a69647c0525c3d34bf94b090dd524
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2018
---
# <a name="install-new-python-packages-on-sql-server"></a>SQL Server 上安裝新的 Python 封裝
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何在 SQL Server 2017 機器學習服務的執行個體上安裝新的 Python 封裝。

一般情況下，安裝新套件的程序是類似於標準的 Python 環境。 不過，一些額外的步驟所需，如果伺服器沒有網際網路連線。

如需了解封裝的安裝位置，或者哪些封裝已安裝的說明，請參閱[檢視安裝的 R 或 Python 封裝](../r/determine-which-packages-are-installed-on-sql-server.md)。

## <a name="prerequisites"></a>필수 구성 요소

+ 您必須安裝機器學習服務 （資料庫） 與 Python 語言選項。 如需指示，請參閱[安裝 SQL Server 2017 機器學習服務 （資料庫）](../install/sql-machine-learning-services-windows-install.md)。

+ 每個伺服器執行個體中，您必須安裝個別封裝的副本。 封裝無法執行個體之間共用。

+ 決定使用 Python 3.5 和 Windows 環境中，您想要使用的封裝是否會運作。 

+ 評估封裝是否適合用來在 SQL Server 環境中使用。 通常資料庫伺服器支援多個服務和應用程式，而且檔案系統上的資源可能會限制，以及連線到伺服器。 在許多情況下是完全封鎖網際網路存取。

    其他常見的問題包括使用的網路上伺服器或防火牆或封裝無法在 Windows 電腦安裝的相依性與封鎖的功能。 

    一些受歡迎的 Python 封裝 （例如酒瓶） 執行工作，例如 web 程式開發更好獨立的環境中執行。 我們建議您使用 Python 資料庫內的工作，例如 machine learning 中，需要大量的資料處理與 database engine 從緊密整合獲益，而不是直接查詢資料庫。

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

    例如，在個別電腦上，您可以下載 WHL 檔案從這個站台[ https://cntk.ai/PythonWheel/CPU-Only ](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)，然後將檔案複製`cntk-2.1-cp35-cp35m-win_amd64.whl`到 SQL Server 電腦上的本機資料夾。

+ SQL Server 2017 使用 Python 3.5。 

> [!IMPORTANT]
> 請確定您取得封裝的 Windows 版本。 如果檔案結尾.gz，很可能不正確的版本。

此頁面包含多個平台與多個的 Python 版本的下載：[設定 CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>步驟 2： 開啟 Python 命令提示字元

找出 SQL Server 所使用的預設 Python 程式庫位置。 如果您已安裝多個執行個體，找出您要加入封裝的執行個體的 PYTHON_SERVICE 資料夾。

例如，如果機器學習服務已安裝，使用預設值，和機器學習服務已啟用預設執行個體上，路徑會，如下所示：

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

開啟 Python 命令提示字元中執行個體相關聯。

> [!TIP]
> 未來偵錯和測試，您可能想要設定 Python 環境的特定執行個體文件庫。

### <a name="step-3-install-the-package-using-pip"></a>步驟 3： 使用 pip 安裝套件

+ 如果您習慣使用 Python 命令列，使用 PIP.exe 來安裝新的封裝。 您可以找到**pip**安裝程式中的`Scripts`子資料夾。 

    如果您收到錯誤，`pip`無法辨識為內部或外部命令，您可以加入的 PATH 變數中 Windows 的 Python 可執行檔和 Python 指令碼資料夾的路徑。

    完整路徑**指令碼**預設安裝中的資料夾如下所示：

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts`

+ 如果您正在使用 Visual Studio 2017 或 Visual Studio 2015 的 Python 擴充功能，您可以執行`pip install`從**Python 環境**視窗。 按一下**封裝**，並在文字方塊中，提供的名稱或要安裝之封裝的位置。 您不需要輸入`pip install`; 它會為您自動填入。 

    - 如果電腦沒有網際網路存取，請提供封裝的名稱或為特定套件和版本的 URL。 
    
    例如，若要安裝的版本支援適用於 Windows 和 Python 3.5 CNTK，指定的下載 URL: `https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - 如果電腦沒有網際網路存取，您必須下載 WHL 檔案開始安裝之前。 然後，指定的本機檔案路徑和名稱。 例如，貼上的下列路徑和檔案，以安裝從網站下載的 WHL 檔案： `"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

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

若要檢視已安裝目前的環境中的 Python 封裝，請從命令提示字元執行這個命令：

```python
conda list
```

如需有關**conda**以及如何使用它來建立和管理多個 Python 環境，請參閱[管理環境與 conda](https://conda.io/docs/user-guide/tasks/manage-environments.html)。
