---
title: 使用 Python 工具來安裝套件
description: 了解如何使用標準的 Python 工具，將新的 Python 套件安裝到 SQL Server 機器學習服務的執行個體。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/21/2020
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 67d5a323cfdbdb7eb765430ba264ff0bde2074f5
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870476"
---
# <a name="install-packages-with-python-tools-on-sql-server"></a>在 SQL Server 上使用 Python 工具來安裝套件
[!INCLUDE [SQL Server 2017 only](../../includes/applies-to-version/sqlserver2017-only.md)]

此文章說明如何使用標準的 Python 工具，在 SQL Server 機器學習服務的執行個體上安裝新的 Python 套件。 一般而言，安裝新套件的程序類似於標準 Python 環境中的程序。 不過，如果伺服器沒有網際網路連線，則需要一些額外步驟。

如需套件位置和安裝路徑的詳細資訊，請參閱[取得 Python 套件資訊](python-package-information.md)。

## <a name="prerequisites"></a>Prerequisites

+ 您必須使用 Python 語言選項安裝 [SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md)。

### <a name="other-considerations"></a>其他考量

+ 套件必須符合 Python 3.5 規範，並可在 Windows 上執行。

+ Python 套件程式庫位於 SQL Server 執行個體的 Program Files 資料夾中，而且根據預設，在此資料夾中安裝需要系統管理員權限。 如需詳細資訊，請參閱[套件程式庫位置](../package-management/python-package-information.md#default-python-library-location)。

+ 套件安裝是按每個執行個體進行。 如果您有多個機器學習服務的執行個體，則必須將套件新增至每一個執行個體。

+ 資料庫伺服器經常會遭到鎖定。 在許多情況下，會完全封鎖網際網路存取。 如果套件所含的相依性清單很長，您必須事先識別這些相依性，並準備好手動安裝每個相依性。

+ 新增套件之前，請考慮套件是否適合用於 SQL Server 環境。

  + 我們建議您在資料庫中使用 Python，以進行與資料庫引擎 (例如機器學習服務) 緊密整合的工作，而不是單純查詢資料庫的工作。

  + 如果您新增的套件為伺服器帶來過多的計算壓力，效能將會受到影響。

  + 在已強化的 SQL Server 環境中，您可以避免下列情況：
    + 需要網路存取的套件
    + 需要提升檔案系統存取權的套件
    + 用於網頁程式開發或其他工作，但無法透過在 SQL Server 內部執行而獲益的套件

## <a name="add-a-python-package-on-sql-server"></a>在 SQL Server 上新增 Python 套件

若要在 SQL Server 上安裝可於指令碼中使用的新 Python 套件，您要在機器學習服務的執行個體中安裝該套件。 如果您有多個機器學習服務的執行個體，則必須將套件新增至每一個執行個體。

下列範例中所安裝的套件是 [CNTK](/cognitive-toolkit/)，此架構適用於進行 Microsoft 所提供的深度學習，可支援自訂、定型及共用不同類型的神經網路。

### <a name="for-offline-install-download-the-python-package"></a>若要離線安裝，請下載 Python 套件

如果您要在無法存取網際網路的伺服器上安裝 Python 套件，您必須從能夠存取網際網路的電腦下載 WHL 檔案，然後將該檔案複製到伺服器。

例如，在連線到網際網路的電腦上，您可以從 `cntk-2.1-cp35-cp35m-win_amd64.whl`[https://cntk.ai/PythonWheel/CPU-Only 網站下載 ](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl) 檔案，然後將該檔案複製到 SQL Server 電腦上的本機資料夾。

> [!IMPORTANT]
> 請確定您取得的是套件的 Windows 版本。 如果檔案的結尾是 .gz，則它可能不是正確的版本。

如需下載適用於多個平台與適用於多個 Python 版本的 CNTK 架構詳細資訊，請參閱[在電腦上安裝 CNTK](/cognitive-toolkit/Setup-CNTK-on-your-machine) \(英文\)。

### <a name="locate-the-python-library"></a>找出 Python 程式庫

找出 SQL Server 所使用的預設 Python 程式庫位置。 如果您已安裝多個執行個體，請找出您想要新增套件之執行個體的 `PYTHON_SERVICES` 資料夾。

例如，如果已使用預設值安裝機器學習服務，而且已在預設執行個體上啟用機器學習，則路徑為：

```console
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES"
```

> [!TIP]
> 針對未來的偵錯及測試，您可以設定執行個體程式庫專屬的 Python 環境。

### <a name="install-the-package-using-pip"></a>使用 pip 來安裝套件

使用 **pip** 安裝程式來安裝新的套件。 您可以在 `pip.exe` 資料夾的 `Scripts` 子資料夾中找到 `PYTHON_SERVICES`。 SQL Server 安裝程式不會將 `Scripts` 子資料夾新增至系統路徑，因此您必須指定完整路徑，或者您也可以將 Scripts 資料夾新增至 Windows 中的 PATH 變數。

> [!NOTE]
> 如果您使用的是 Visual Studio 2017 或含有 Python 延伸模組的 Visual Studio 2015，您可以從 [Python 環境]`pip install`**視窗中執行**。 按一下 [套件]  ，然後在文字方塊中提供要安裝之套件的名稱或位置。 您不需要輸入 `pip install`；系統會自動為您填入。

+ 如果電腦能夠存取網際網路，請提供套件的名稱：

  ```console
  scripts\pip.exe install cntk
  ```
  您也可以指定特定套件與版本的 URL，例如：

  ```console
  scripts\pip.exe install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  ```

+ 如果電腦無法存取網際網路，請指定您稍早下載的 WHL 檔案。 例如：

  ```console
  scripts\pip.exe install C:\Downloads\cntk-2.1-cp35-cp35m-win_amd64.whl
  ```

系統可能會提示您提高權限以完成安裝。
在安裝過程中，您可以在命令提示字元視窗中看到狀態訊息。

### <a name="load-the-package-or-its-functions-as-part-of-your-script"></a>載入套件或其函式作為指令碼的一部分

安裝完成之後，您就能在 SQL Server 中的 Python 指令碼中立即開始使用套件。

若要在指令碼中使用套件的函式，請在指令碼的前幾行中插入標準的 `import <package_name>` 陳述式：

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
import cntk
# Python statements ...
'
```

## <a name="see-also"></a>另請參閱

+ [取得 Python 套件資訊](python-package-information.md)
+ [SQL Server 機器學習服務的 Python 教學課程](../tutorials/python-tutorials.md)
+ [適用於 CNTK 的 Python API](https://cntk.ai/pythondocs/tutorials.html) \(英文\)。