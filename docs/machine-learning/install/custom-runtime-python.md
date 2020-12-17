---
title: 安裝 Python 自訂執行階段
description: 了解如何安裝 SQL Server 適用的 Python 自訂執行階段。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/20/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 15047969fdf25727d324ae577414273cc86769cf
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471219"
---
# <a name="install-a-python-custom-runtime-for-sql-server"></a>安裝 SQL Server 適用的 Python 自訂執行階段
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

本文說明如何安裝自訂執行階段，以使用 SQL Server 執行 Python 指令碼。 自訂執行階段使用以擴充性架構為基礎的語言延伸模組技術來執行外部程式碼。 Python 適用的自訂執行階段可用於下列案例：

+ 安裝具備擴充性架構的 SQL Server。

+ 安裝 SQL Server 2019 機器學習服務。 完成一些額外的設定步驟後，可搭配 [SQL Server 機器學習服務](../sql-server-machine-learning-services.md)使用語言延伸模組。

::: moniker range=">=sql-server-ver15"

> [!NOTE]
> 本文說明如何在 Windows 上安裝 Python 適用的自訂執行階段。 若要在 Linux 上安裝，請查看[如何在 Linux 上安裝 SQL Server 適用的 Python 自訂執行階段](custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true)。

## <a name="pre-install-checklist"></a>預先安裝檢查清單

安裝 Python 自訂執行階段之前，請先安裝下列項目：

+ [適用於 Windows 的 SQL Server 2019 累積更新 (CU) 3](../../database-engine/install-windows/install-sql-server.md)。

+ [Windows 上具備擴充性架構的 SQL Server 語言延伸模組](../../language-extensions/install/windows-java.md)。

+ [Python 3.7]( https://www.python.org/downloads/release/python-379/)。

## <a name="add-sql-server-language-extensions-for-windows"></a>新增 Windows 適用的 SQL Server 語言延伸模組

> [!NOTE]
> 如果您已在 SQL Server 2019 上安裝了機器學習服務，便已經安裝擴充性架構，可略過此步驟。

語言延伸模組會使用擴充性架構來執行外部程式碼。 程式碼執行與核心引擎流程隔離，但與 SQL Server 查詢執行完全整合。

1. 啟動 SQL Server 2019 的安裝精靈。
  
1. 在 [安裝]  索引標籤上，選取 [新增 SQL Server 獨立安裝或將功能加入至現有安裝]  。
    
    ![SQL Server 2019 安裝 CU3 或更新版本](../install/media/2019setup-installation-page-mlsvcs.png) 

1. 在 [特徵選取]  頁面上，選取下列選項：
  
    - **Database Engine 服務**
  
        若要搭配 SQL Server 使用語言延伸模組，您必須安裝資料庫引擎的執行個體。 您可以使用預設或具名執行個體。
  
    - **機器學習服務和語言延伸模組**
   
       選取 [機器學習服務和語言延伸模組]。 不需要選取 [Python]。

    ![SQL Server 2019 CU3 或更新版本安裝功能](../install/media/sql-feature-selection.png) 

1. 在 [準備安裝]  頁面上，確認包含這些選項，然後選取 [安裝]  。
  
    + Database Engine 服務
    + 機器學習服務和語言延伸模組

1. 在安裝程式完成之後，如果系統要求您重新啟動電腦，請立即重新啟動。 當您完成安裝時，請務必閱讀安裝精靈所提供的訊息。 如需詳細資訊，請參閱＜ [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)＞。


## <a name="install-python-37"></a>安裝 Python 3.7 

安裝 [Python 3.7]( https://www.python.org/downloads/release/python-379/)，並將其新增至路徑。

![將 Python 3.7 新增至路徑。](../install/media/python-379.png) 


#### <a name="install-pandas"></a>安裝 pandas

從 *已提升權限的* 命令提示字元中，安裝 Python 適用的 [pandas](https://pandas.pydata.org/) 套件：

```bash
python.exe -m pip install pandas
```

## <a name="update-the-system-environment-variables"></a>更新系統環境變數

新增或修改 PYTHONHOME，做為系統環境變數。

+ 在 Windows 搜尋方塊中，輸入「環境」，然後選取 [編輯系統環境變數]。
+ 在 [進階] 索引標籤中，選取 [環境變數]。
+ 在 [系統變數] 底下選取 [新增]，以建立指向 Python 3.7 安裝位置的 PYTHONHOME。
如果 PYTHONHOME 已存在，請選取 [編輯]，將其指向 Python 3.7 安裝位置。
+ 選取 [確定] 關閉其餘視窗。

![建立 PYTHONHOME 系統變數。](../install/media/sys-pythonhome.png)

## <a name="grant-access-to-the-custom-python-installation-folder"></a>授與自訂 Python 安裝資料夾的存取權

從全新 *已提升權限的* 命令提示字元執行下列 **icacls** 命令，將 PYTHONHOME 的讀取和執行權限授與 **SQL Server Launchpad 服務** 和 SID **S-1-15-2-1** (**ALL_APPLICATION_PACKAGES**)。 Launchpad 服務使用者名稱 `NT Service\MSSQLLAUNCHPAD$INSTANCENAME* where INSTANCENAME` 是 SQL Server 的執行個體名稱。 這些命令會以遞迴方式授與指定目錄路徑下的所有檔案與資料夾的存取權。

將執行個體名稱附加至 `MSSQLLAUNCHPAD` (`MSSQLLAUNCHPAD$INSTANCENAME`)。 在此範例中，INSTANCENAME 是預設執行個體`MSSQLSERVER`。

1. 授與權限給 **SQL Server Launchpad 服務使用者名稱**。

    ```cmd
    icacls "%PYTHONHOME%" /grant "NT Service\MSSQLLAUNCHPAD$MSSQLSERVER":(OI)(CI)RX /T

2. Give permissions to **SID S-1-15-2-1**.
    ```cmd
    icacls "%PYTHONHOME%" /grant *S-1-15-2-1:(OI)(CI)RX /T

>[!NOTE]
>The preceding command grants permissions to the computer **SID S-1-15-2-1**, which is equivalent to ALL APPLICATION PACKAGES on an English version of Windows. Alternatively, you can use `icacls "%R_HOME%" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` on an English version of Windows.

## Restart SQL Server Launchpad service

From an *elevated* command prompt, run the following commands. Replace "MSSQLSERVER" with the name of your SQL Server instance.

```CMD
net stop MSSQLLAUNCHPAD$MSSQLSERVER
net start MSSQLLAUNCHPAD$MSSQLSERVER
```

也可以在系統的 **服務** 應用程式中用滑鼠右鍵按一下 [SQL Server Launchpad] 服務，然後按一下 [重新啟動] 命令。 或使用 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md) 來重新啟動服務。

## <a name="download-python-language-extension"></a>下載 Python 語言延伸模組

下載[包含適用於 Windows 之 Python 語言延伸模組的 ZIP 檔案](https://github.com/microsoft/sql-server-language-extensions/releases) \(英文\)。 建議在生產環境中使用發行版本。 在開發或測試時使用偵錯版本，因為其提供詳細的記錄資訊，可供您調查任何錯誤。

## <a name="register-external-language"></a>註冊外部語言

針對您要使用的每個資料庫，使用 [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) 來註冊此 Python 語言延伸模組。 使用 [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) 連線到 SQL Server 並執行下列的 T-SQL 命令。 修改此陳述式中的路徑，以反映下載的語言延伸模組 zip 檔案 (python-lang-extension.zip) 的位置。

> [!NOTE]
> Python 是保留的字組。 請針對外部語言使用不同的名稱，例如 myPython。

```sql
CREATE EXTERNAL LANGUAGE [myPython]
FROM (CONTENT = N'/path/to/python-lang-extension.zip', FILE_NAME = 'pythonextension.dll');
GO
```

::: moniker-end

::: moniker range=">=sql-server-linux-ver15"

您可在 Red Hat Enterprise Linux (RHEL)、SUSE Linux Enterprise Server (SLES) 和 Ubuntu 上安裝 SQL Server。 如需詳細資訊，請參閱 [Linux 上的 SQL Server 安裝指引](../../linux/sql-server-linux-setup.md)中的＜支援的平台＞一節。

> [!NOTE]
> 本文說明如何在 Linux 上安裝 Python 適用的自訂執行階段。 若要在 Windows 上安裝，請查看[在 Windows 上安裝 SQL Server 適用的 Python 自訂執行階段](custom-runtime-python.md?view=sql-server-ver15&preserve-view=true)

## <a name="pre-install-checklist"></a>預先安裝檢查清單

安裝 Python 自訂執行階段之前，請先安裝下列項目：

+ [Linux 適用的 SQL Server 2019 (累積更新 3 或更新版本)](../../linux/sql-server-linux-setup.md)。
當您在 Linux 上安裝 SQL Server 時，您必須設定 Microsoft 存放庫。 如需詳細資訊，請參閱[設定存放庫](../../linux/sql-server-linux-change-repo.md)

  > [!NOTE]
  > Python 自訂執行階段需要 SQL Server 2019 的累積更新 (CU) 3 或更新版本。

+ [Linux 上具備擴充性架構的 SQL Server 語言延伸模組](../../linux/sql-server-linux-setup-language-extensions-java.md)。

+ [Python 3.7](https://www.python.org/downloads/release/python-379/)。

## <a name="add-sql-server-language-extensions-for-linux"></a>新增 Linux 適用的 SQL Server 語言延伸模組

> [!NOTE]
> 如果您已在 SQL Server 2019 上安裝了機器學習服務，便已經安裝語言延伸模組適用的 **mssql-server-extensibility** 套件，可略過此步驟。

語言延伸模組會使用擴充性架構來執行外部程式碼。 程式碼執行與核心引擎流程隔離，但與 SQL Server 查詢執行完全整合。

使用下列命令，根據您的 Linux 版本安裝語言延伸模組。

### <a name="ubuntu"></a>Ubuntu
> [!TIP]
> 可能的話，請在安裝之前`update`，以重新整理系統上的套件。 Ubuntu 可能沒有 HTTPs apt 傳輸選項。 若要安裝它，請使用 `apt-get install apt-transport-https`。

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility
```

### <a name="red-hat"></a>Red Hat
```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility
```

### <a name="suse"></a>Suse
```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility
```

## <a name="install-python-37-and-pandas"></a>安裝 Python 3.7 和 pandas

安裝 Python 3.7、libpython 3.7 程式庫和 pandas 套件。 

以下是 Ubuntu 適用的範例命令：

```bash
# Install python3.7 and the corresponding library:
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.7 python3-pip libpython3.7

# Install pandas to /usr/lib:
sudo python3.7 -m pip install pandas -t /usr/lib/python3.7/dist-packages
```

## <a name="using-a-custom-installation-of-python-37"></a>使用 Python 3.7 的自訂安裝

> [!NOTE]
> 如果您已在 `/usr/lib/python3.7` 的預設位置安裝 Python，您可以跳到[下一節](#download-python-linux)。

如果您已建立自己的 Python 3.7 版本，請使用下列命令，讓 SQL Server 可以尋找並載入您的自訂安裝。

### <a name="update-the-environment-variables"></a>更新環境變數

1. 編輯 mssql-launchpadd 服務，將 PYTHONHOME 環境變數新增至檔案 `/etc/systemd/system/mssql-launchpadd.service.d/override.conf`

      ```bash
      sudo systemctl edit mssql-launchpadd
      ```

    + 在開啟的 `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` 檔案中插入下列文字。 將 PYTHONHOME 的值設定為自訂 Python 安裝路徑。

      ```vi
      [Service]
      Environment="PYTHONHOME=/path/to/installation/of/python3.7"
      ```

    + 儲存並關閉。

2. 請確定可以載入 `libpython3.7m.so.1.0`。

    + 在 `/etc/ld.so.conf.d` 中建立 custom-python.conf 檔案。

      ```bash
      sudo vi /etc/ld.so.conf.d/custom-python.conf
      ```

    + 在開啟的檔案中，從自訂 Python 安裝新增 **libpython3.7m.so.1.0** 的路徑。

      ```vi
      /path/to/installation/of/python3.7/lib
      ```

    + 儲存並關閉新檔案。

    + 執行下列命令，並檢查是否找得到所有相依的程式庫，以執行 `ldconfig` 並確認可以載入 `libpython3.7m.so.1.0`。

      ```bash
      sudo ldconfig
      ldd /path/to/installation/of/python3.7/lib/libpython3.7m.so.1.0
      ```

### <a name="grant-access-to-the-custom-python-folder"></a>授與自訂 Python 資料夾的存取權

在 /var/opt/mssql/mssql.conf 檔案的 [擴充性] 區段中，將 `datadirectories` 選項設定為自訂 python 安裝。

```bash
sudo /opt/mssql/bin/mssql-conf set extensibility.datadirectories /path/to/installation/of/python3.7
```

### <a name="restart-the-mssql-launchpadd-service"></a>重新啟動 mssql-launchpadd 服務

```bash
sudo systemctl restart mssql-launchpadd
```
## <a name="download-python-language-extension"></a><a name="download-python-linux"></a> 下載 Python 語言延伸模組

下載[包含適用於 Linux 之 Python 語言延伸模組的 ZIP 檔案](https://github.com/microsoft/sql-server-language-extensions/releases) \(英文\)。 建議在生產環境中使用發行版本。 在開發或測試時使用偵錯版本，因為其提供詳細的記錄資訊，可供您調查任何錯誤。

## <a name="register-external-language"></a>註冊外部語言

針對您要使用的每個資料庫，使用 [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) 來註冊此 Python 語言延伸模組。 使用 [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) 連線到 SQL Server 並執行下列的 T-SQL 命令。 
修改此陳述式中的路徑，以反映下載的語言延伸模組 zip 檔案 (python-lang-extension.zip) 的位置。

> [!NOTE]
>Python 是保留的字組。 請針對外部語言使用不同的名稱，例如 myPython。

```sql
CREATE EXTERNAL LANGUAGE myPython 
FROM (CONTENT = N'/PATH/TO/python-lang-extension.zip', FILE_NAME = 'libPythonExtension.so.1.0');
GO
```

::: moniker-end

## <a name="enable-external-script-execution-in-sql-server"></a>啟用 SQL Server 中的外部指令碼執行

您可以透過針對 SQL Server 執行的預存程序 [sp_execute_external script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 來執行 Python 中的外部指令碼。 

若要啟用外部指令碼，請使用連線至 SQL Server 的 [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) 來執行下列 SQL 命令。

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

## <a name="verify-language-extension-installation"></a>驗證語言延伸模組安裝

此 SQL 指令碼會測試已安裝的語言延伸模組功能。

```sql
EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
import sys
print(sys.path)
print(sys.version)
print(sys.executable)'
```

## <a name="verify-parameters-and-datasets-of-different-data-types"></a>驗證不同資料類型的參數和資料集

此指令碼會針對輸入/輸出參數和資料集來測試不同的資料類型。

```sql
DECLARE @sumVal int = 12;
DECLARE @charVal VARCHAR(30) = N'Hello'

EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
print(sumVal)
print(charVal)
sumVal = sumVal + 300
OutputDataSet = InputDataSet'
,@input_data_1 = N'SELECT 1, CAST(1.4 as real), ''Hi'', CAST(''1'' as bit)'
,@params = N'@sumVal int OUTPUT, @charVal VARCHAR(30)'
,@sumVal = @sumVal OUTPUT
,@charVal = @charVal
WITH RESULT SETS ((intCol int, doubleCol real, charCol char(2), logicalCol bit));

PRINT @sumVal
```

## <a name="next-steps"></a>後續步驟

+ [SQL Server 中的擴充性架構](../concepts/extensibility-framework.md)
+ [語言延伸模組概觀](../../language-extensions/language-extensions-overview.md)
