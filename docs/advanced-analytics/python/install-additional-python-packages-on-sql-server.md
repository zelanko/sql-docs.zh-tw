---
title: 安裝新的 Python 語言套件-SQL Server Machine Learning
description: 將新的 Python 套件新增至 SQL Server 2017 Machine Learning 服務 （資料庫內） 和 Machine Learning Server （獨立式）。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: cc83ed8500e93147163e3166b895c7333b4222cd
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510295"
---
# <a name="install-new-python-packages-on-sql-server"></a>SQL Server 上安裝新的 Python 套件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何在 SQL Server 2017 Machine Learning 服務的執行個體上安裝新的 Python 套件。 一般情況下，安裝新套件的程序是類似於標準的 Python 環境。 不過，一些額外的步驟所需，如果伺服器沒有網際網路連線。

如需封裝的位置和安裝路徑的詳細資訊，請參閱 <<c0> [ 取得 R 或 Python 封裝資訊](../r/determine-which-packages-are-installed-on-sql-server.md)。

## <a name="prerequisites"></a>先決條件

+ [SQL Server 2017 Machine Learning 服務 （資料庫）](../install/sql-machine-learning-services-windows-install.md)與 Python 語言選項。 

+ 套件必須是 Windows 上的 Python 3.5 相容和執行。 

+ 系統管理伺服器的存取權才可安裝套件。

## <a name="considerations"></a>考量

然後再加入封裝，請考慮封裝是否適用於 SQL Server 環境。 通常資料庫伺服器是配合多個工作負載的共用的資產。 如果您新增的壓力，太多計算伺服器的封裝，將會降低效能。 

此外，一些熱門的 Python 套件 （例如 Flask) 執行工作，例如 web 開發、 計較適合用來獨立環境。 我們建議您在資料庫引擎，例如機器學習服務，而獲益的緊密整合的工作，而不是直接查詢資料庫的工作使用 Python 中的資料庫。

資料庫伺服器經常被鎖定。 在許多情況下，會完全封鎖網際網路存取。 針對具有一長串的相依性套件，您必須事先識別這些相依性，並願意手動安裝每個。

## <a name="add-a-new-python-package"></a>新增新的 Python 封裝

此範例中，我們假設您想要直接在 SQL Server 電腦上安裝新套件。

安裝套件是每個執行個體。 如果您有多個機器學習服務執行個體時，您必須新增封裝到每一個。

在此範例中所安裝的套件[CNTK](https://docs.microsoft.com/cognitive-toolkit/)，來自 Microsoft 的支援自訂項目，教育訓練，以及不同類型的類神經網路共用的深度學習架構。

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>步驟 1： 下載 Windows 版本的 Python 套件

+ 如果您要在沒有網際網路存取伺服器上安裝 Python 套件，您必須下載到不同的電腦的 WHL 檔案，並再將它複製到伺服器。

    比方說，在另一部電腦，您可以下載的 WHL 檔案從這個站台[ https://cntk.ai/PythonWheel/CPU-Only ](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)，然後將檔案複製`cntk-2.1-cp35-cp35m-win_amd64.whl`到 SQL Server 電腦上的本機資料夾。

+ SQL Server 2017 會使用 Python 3.5。 

> [!IMPORTANT]
> 請確定您取得封裝的 Windows 版本。 如果檔案結尾.gz，很可能不正確的版本。

此頁面包含多個平台以及多個 Python 版本的下載項目：[設定 CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>步驟 2： 開啟 Python 命令提示字元

找出 SQL Server 所使用的預設 Python 程式庫位置。 如果您已安裝多個執行個體，找出您要加入封裝的執行個體 PYTHON_SERVICE 資料夾。

例如，如果已安裝 Machine Learning 服務使用預設值，以及機器學習服務已啟用預設執行個體上，路徑為，如下所示：

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

開啟 Python 命令提示字元中執行個體相關聯。

> [!TIP]
> 未來偵錯和測試，您可能想要設定的 Python 環境的特定執行個體文件庫。

### <a name="step-3-install-the-package-using-pip"></a>步驟 3： 使用 pip 安裝套件

+ 如果您習慣使用 Python 命令列時，可用於 PIP.exe 安裝新的套件。 您可以找到**pip**中的安裝程式`Scripts`子資料夾。 

  SQL Server 安裝程式不會新增至系統路徑的指令碼。 如果您收到錯誤指出`pip`無法辨識為內部或外部命令，您可以將指令碼 資料夾加入 PATH 變數，在 Windows 中。

  完整路徑**指令碼**資料夾在預設安裝中如下所示：

    C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts

+ 如果您使用 Visual Studio 2017 或 Visual Studio 2015 使用 Python 擴充功能，您可以執行`pip install`從**Python 環境**視窗。 按一下 **封裝**，並在文字方塊中，提供的名稱或要安裝之封裝的位置。 您不需要輸入`pip install`; 它會為您自動填入。 

    - 如果電腦沒有網際網路存取，提供封裝的名稱或為特定的套件和版本的 URL。 
    
    例如，若要安裝 CNTK 支援 Windows 及 Python 3.5 的版本，指定的下載 URL: `https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - 如果電腦沒有網際網路存取，您必須在開始安裝之前下載的 WHL 檔案。 然後，指定的本機檔案路徑和名稱。 比方說，貼上下列的路徑和檔案，以安裝從網站下載的 WHL 檔案： `"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

您可能會提示提升權限來完成安裝。

安裝進行時，您可以看到 [命令提示字元] 視窗中的狀態訊息：

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>步驟 4： 在您的指令碼載入封裝或其函式

安裝完成時，您可以立即開始使用的封裝下, 一個步驟中所述。

如需使用 CNTK 的深度學習的範例，請參閱這些教學課程：[Cntk Python API](https://cntk.ai/pythondocs/tutorials.html)

若要使用封裝中的函式，在您的指令碼中，插入標準`import <package_name>`陳述式中的指令碼前面幾行：

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>列出已安裝的套件使用 conda

有不同的方式，您可以取得一份已安裝的套件。 例如，您可以檢視在已安裝的套件**Python 環境**的 Visual Studio 的 windows。

如果您使用 Python 命令列，您可以使用**Pip**或**conda**套件管理員 中，隨附於 SQL Server 安裝程式新增的 Anaconda Python 環境。

1. 請移至 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Scripts

1. 以滑鼠右鍵按一下**conda.exe** > **系統管理員身分執行**，然後輸入`conda list`來傳回目前環境中安裝的套件清單。

1. 同樣地，以滑鼠右鍵按一下**pip.exe** > **系統管理員身分執行**，然後輸入`pip list`傳回相同的資訊。 

如需詳細資訊**conda**以及如何使用它來建立和管理多個 Python 環境，請參閱[管理 conda 環境](https://conda.io/docs/user-guide/tasks/manage-environments.html)。

> [!Note]
> SQL Server 安裝程式不會新增 Pip 或 Conda 至系統路徑和實際執行 SQL Server 的執行個體，讓非必要的可執行檔的路徑之外是最佳作法。 不過，開發和測試環境中，您可以將指令碼 資料夾加入系統的 PATH 環境變數，從任何位置執行 Pip 和 Conda 命令。
