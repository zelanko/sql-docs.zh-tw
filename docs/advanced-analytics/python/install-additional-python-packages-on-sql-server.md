---
title: 安裝新的 Python 語言套件
description: 將新的 Python 套件新增至 SQL Server 2017 Machine Learning 服務 (資料庫內) 和 Machine Learning Server (獨立式)。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/16/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: fc8c7148369ec1a501106e573e195a8f0b7f060a
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470261"
---
# <a name="install-new-python-packages-on-sql-server"></a>在 SQL Server 上安裝新的 Python 套件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何在 SQL Server 2017 Machine Learning 服務的實例上安裝新的 Python 套件。 一般而言, 安裝新套件的程式類似于標準 Python 環境中。 不過, 如果伺服器沒有網際網路連線, 則需要一些額外的步驟。

如需套件位置和安裝路徑的詳細資訊, 請參閱[取得 R 或 Python 套件資訊](../package-management/installed-package-information.md)。

## <a name="prerequisites"></a>先決條件

+ 使用 Python 語言選項[SQL Server 2017 Machine Learning 服務 (資料庫內)](../install/sql-machine-learning-services-windows-install.md) 。 

+ 套件必須符合 Python 3.5 規範, 並可在 Windows 上執行。 

+ 必須要有伺服器的系統管理存取權, 才能安裝封裝。

## <a name="considerations"></a>考量

在新增封裝之前, 請考慮套件是否適合用於 SQL Server 環境。 資料庫伺服器通常是可容納多個工作負載的共用資產。 如果您新增的封裝在伺服器上放置過多的計算壓力, 效能將會受到影響。 

此外, 某些熱門的 Python 套件 (例如 Flask) 會執行更適合獨立環境的工作, 如 web 程式開發。 我們建議您在資料庫中使用 Python, 以進行與資料庫引擎緊密整合 (例如機器學習服務) 的工作, 而不是單純查詢資料庫的工作。

資料庫伺服器經常被鎖定。 在許多情況下, 會完全封鎖網際網路存取。 針對具有較長相依性清單的套件, 您必須事先識別這些相依性, 並願意手動安裝每個相依性。

## <a name="add-a-new-python-package"></a>新增 Python 套件

在此範例中, 我們假設您想要直接在 SQL Server 電腦上安裝新的套件。

套件安裝是每個實例。 如果您有多個 Machine Learning 服務實例, 則必須將封裝新增至每一個。

在此範例中安裝的套件是[CNTK](https://docs.microsoft.com/cognitive-toolkit/), 這是一種適用于 Microsoft 的深度學習架構, 可支援自訂、訓練和共用不同類型的類神經網路。

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>步驟 1： 下載 Python 套件的 Windows 版本

+ 如果您要在沒有網際網路存取的伺服器上安裝 Python 套件, 您必須將 .WHL 檔案下載到不同的電腦, 然後將它複製到伺服器。

    例如, 在另一部電腦上, 您可以從這個網站[https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)下載 .whl 檔案, 然後將檔案複製`cntk-2.1-cp35-cp35m-win_amd64.whl` 到 SQL Server 電腦上的本機資料夾。

+ SQL Server 2017 使用 Python 3.5。 

> [!IMPORTANT]
> 請確定您取得套件的 Windows 版本。 如果檔案的結尾是 gz, 它可能不是正確的版本。

此頁面包含適用于多個平臺和多個 Python 版本的下載:[設定 CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>步驟 2： 開啟 Python 命令提示字元

找出 SQL Server 所使用的預設 Python 程式庫位置。 如果您已安裝多個實例, 請找出您想要新增封裝之實例的 PYTHON_SERVICE 資料夾。

例如, 如果 Machine Learning 服務已使用預設值安裝, 而且預設實例上已啟用機器學習, 則路徑會如下所示:

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

開啟與實例相關聯的 Python 命令提示字元。

> [!TIP]
> 針對未來的偵錯工具和測試, 您可能會想要設定實例程式庫專屬的 Python 環境。

### <a name="step-3-install-the-package-using-pip"></a>步驟 3： 使用 pip 安裝套件

+ 如果您習慣使用 Python 命令列, 請使用 PIP 來安裝新的封裝。 您可以在`Scripts`子資料夾中找到**pip**安裝程式。 

  SQL Server 安裝程式不會將腳本新增至系統路徑。 如果您收到無法辨識為`pip`內部或外部命令的錯誤, 您可以將 Scripts 資料夾新增至 Windows 中的 PATH 變數。

  在預設安裝中,**腳本**資料夾的完整路徑如下所示:

    C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts

+ 如果您使用 Visual Studio 2017, 或 Visual Studio 2015 搭配 python 延伸模組, 您可以從 [ `pip install` **python 環境**] 視窗執行。 按一下 [**套件**], 然後在文字方塊中提供要安裝之封裝的名稱或位置。 您不需要輸入`pip install`, 系統會自動為您填入。 

    - 如果電腦可以存取網際網路, 請提供封裝的名稱, 或特定封裝和版本的 URL。 
    
    例如, 若要安裝 Windows 和 Python 3.5 支援的 CNTK 版本, 請指定下載 URL:`https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - 如果電腦無法存取網際網路, 您必須先下載 .WHL 檔案, 然後再開始安裝。 然後, 指定本機檔案路徑和名稱。 例如, 請貼上下列路徑和檔案, 以安裝從網站下載的 .WHL 檔案:`"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

系統可能會提示您提高許可權以完成安裝。

當安裝進行時, 您可以在 [命令提示字元] 視窗中看到狀態訊息:

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>步驟 4： 載入封裝或其函式作為腳本的一部分

安裝完成時, 您可以立即開始使用封裝, 如下一個步驟所述。

如需使用 CNTK 進行深度學習的範例, 請參閱下列教學課程:[適用于 CNTK 的 Python API](https://cntk.ai/pythondocs/tutorials.html)

若要在腳本中使用套件中的函式, 請`import <package_name>`在腳本的初始行中插入標準語句:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>使用 conda 列出已安裝的套件

有不同的方式可讓您取得已安裝套件的清單。 例如, 您可以在 Visual Studio 的 [ **Python 環境**] 視窗中, 查看已安裝的套件。

如果您使用的是 Python 命令列, 您可以使用**Pip**或**conda**套件管理員 (隨附于 SQL Server 安裝程式所新增的 Anaconda Python 環境中)。

1. 移至 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Scripts

1. 以滑鼠右鍵按一下 [ **conda**  > ] [以**系統管理員**身分`conda list`執行], 然後輸入以傳回目前環境中所安裝的套件清單。

1. 同樣地, 以滑鼠右鍵按一下 [ **pip**  > ] [以**系統管理員身分執行**], 然後輸入`pip list`以傳回相同的資訊。 

如需**conda**以及如何使用它來建立和管理多個 Python 環境的詳細資訊, 請參閱[使用 conda 管理環境](https://conda.io/docs/user-guide/tasks/manage-environments.html)。

> [!Note]
> SQL Server 安裝程式不會在系統路徑和生產 SQL Server 實例上新增 Pip 或 Conda, 因此最佳做法是將非必要的可執行檔保留在路徑外。 不過, 針對開發和測試環境, 您可以將 Scripts 資料夾新增至系統 PATH 環境變數, 以從任何位置執行 Pip 和 Conda on 命令。
