---
title: 升級 Python 和 R 執行階段 (繫結)
description: 使用 sqlbindr.exe 升級 SQL Server 機器學習服務或 SQL Server R Services 中的 Python 和 R 執行階段，以繫結至 Machine Learning Server。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/30/2020
ms.topic: how-to
author: cawrites
ms.author: chadam
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 2036fda1d483bdfb04a205f5a2e3bf6d86119b1b
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956723"
---
# <a name="upgrade-python-and-r-runtime-with-binding-in-sql-server-machine-learning-services"></a>使用繫結在 SQL Server 機器學習服務中升級 Python 和 R 執行階段
[!INCLUDE [SQL Server 2016 and 2017](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

本文說明如何使用名為**繫結**的安裝程序，在 [SQL Server 2016 R Services](../r/sql-server-r-services.md) 或 [SQL Server 2017 機器學習服務](../sql-server-machine-learning-services.md)中升級 R 或 Python 執行階段。 您可以透過「繫結」至 [Microsoft Machine Learning Server](/machine-learning-server)，取得 [Python 和 R 的較新版本](#version-map)。

> [!IMPORTANT]
> 本文說明用來升級 R 和 Python 執行階段的舊方法，名為*繫結*。 如果您已安裝 **SQL Server 2016 Services Pack (SP) 2 的累積更新 (CU) 14 或更新版本**，或 **SQL Server 2017 的累積更新 (CU) 22 或更新版本**，則應參閱如何[將預設的 R 或 Python 語言執行階段變更為更新版本](change-default-language-runtime-version.md)。

## <a name="what-is-binding"></a>何謂繫結？

繫結是一種安裝程序，會使用來自 [Microsoft Machine Learning Server](/machine-learning-server) 的較新的可執行檔、程式庫與工具，取代 **R_SERVICES** 與 **PYTHON_SERVICES** 資料夾的內容。

維護模型所包含的上傳元件已經變更。 服務更新現在符合[現代化生命週期](https://support.microsoft.com/help/30881/modern-lifecycle-policy)上的 [Microsoft R Server 與 Machine Learning Server 支援時間表](/machine-learning-server/resources-servicing-support) \(英文\)。

除了元件版本和服務更新以外，繫結不會變更安裝的基礎：

- Python 和 R 整合仍然是資料庫引擎執行個體的一部分。
- 授權不變 (沒有額外成本與繫結相關聯)。
- SQL Server 支援原則仍然適用於資料庫引擎。

本文的其餘部分將說明繫結機制，以及它針對每個版本的 SQL Server 的運作方式。

> [!NOTE]
> 繫結僅適用於繫結至 SQL Server 執行個體的資料庫內執行個體。 在此情況下，獨立安裝不需要繫結。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**SQL Server 2016 繫結考量**

針對 SQL Server 2016 R Services 客戶，繫結提供：

- 已更新的 R 套件。
- 不是原始安裝 ([MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) \(英文\)) 一部分的新套件
- 適用於情感分析和影像偵測的預先定型機器學習[模型](/machine-learning-server/install/microsoftml-install-pretrained-models)。

所有繫結都可以在 [Microsoft Machine Learning Server](/machine-learning-server/index) \(英文\) 的每個新主要和次要版本推出時進一步重新整理。
::: moniker-end

## <a name="version-map"></a>版本對應

下表為版本對應。 每個對應都顯示所有版本的套件版本。 當您繫結至 Microsoft Machine Learning Server (在 Microsoft Machine Learning Server 9.2.1 開始加入 Python 支援之前稱為 R Server) 時，可以檢閱升級路徑。

繫結不保證 R 或 Anaconda 的最新版本。 當您繫結至 Microsoft Machine Learning Server 時，您可以透過安裝程式安裝 R 或 Python 版本，安裝程式可能不是 Web 上可取得的最新版本。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

元件 |初始版本 | [R Server 9.0.1](/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](/machine-learning-server/install/r-server-install-windows) | [Machine Learning Server 9.2.1](/machine-learning-server/install/machine-learning-server-windows-install) \(英文\) | [Machine Learning Server 9.3](/machine-learning-server/install/machine-learning-server-windows-install) \(英文\) |  [Machine Learning Server 9.4.7](/machine-learning-server/install/machine-learning-server-windows-install) \(英文\)
----------|----------------|----------------|--------------|---------|-------|-------|
Microsoft R Open (MRO) (R) | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 | R 3.5.2
[RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |  9.4.7 |
[MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 | 9.4.7 |
[預先定型的模型](/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 | 9.4.7 |
[sqlrutils](/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 | 1.0 |
[olapR](/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 | 1.0 |
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
[**SQL Server 2017 機器學習服務**](../install/sql-machine-learning-services-windows-install.md)

元件 |初始版本 | Machine Learning Server 9.3 | Machine Learning Server 9.4.7 |
----------|----------------|---------|---------|
Microsoft R Open (MRO) (R) | R 3.3.3 | R 3.4.3 | R 3.5.2 |
[RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | 9.4.7 |
[MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| 9.4.7 |
[sqlrutils](/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | 1.0 |
[olapR](/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | 1.0 |
Anaconda 4.2 (Python 3.5)  | 4.2/3.5.2 | 4.2/3.5.2 |
[revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| 9.4.7 |
[microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| 9.4.7 |
[預先定型的模型](/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| 9.4.7 |
::: moniker-end

## <a name="how-component-upgrade-works"></a>元件升級的運作方式

當您將現有的 Python 和 R 安裝繫結至 Machine Learning Server 時，可執行檔、Python 和 R 程式庫都會升級。

當您在具有 Python 或 R 整合的現有 SQL Server 資料庫引擎執行個體上執行安裝程式時，[Microsoft Machine Learning Server 安裝程式](/machine-learning-server/install/machine-learning-server-windows-install) \(英文\) 會執行繫結。 

安裝程式會偵測現有的功能，並提示您重新繫結至 Machine Learning Server。

在繫結期間，`C:\Program Files\Microsoft\ML Server\R_SERVER` 和 `\PYTHON_SERVER` 的較新可執行檔和程式庫，會覆寫 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` 和 `\PYTHON_SERVICES` 的內容。

繫結僅適用於 Python 和 R 功能。 Python 和 R 的開放原始碼套件由下列項目組成：

- Anaconda
- Microsoft R Open
- 專屬套件 RevoScaleR
- Revoscalepy

繫結不會變更資料庫引擎執行個體的支援模型或 SQL Server 的版本。

繫結是可還原的。 您可以藉由[解除繫結執行個體](#bkmk_Unbind)並修復 SQL Server 資料庫引擎執行個體來還原為 SQL Server 服務。

<a name="bkmk_BindWizard"></a>

## <a name="bind-to-machine-learning-server-using-setup"></a>使用安裝程式繫結至 Machine Learning Server

請遵循步驟，使用安裝程式將 SQL Server 繫結至 Microsoft Machine Learning Server。 

1. 在 SSMS 中，執行 `SELECT @@version` 以確認伺服器符合最低組建需求。

   針對 SQL Server 2016 R Services，最低為 [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) 和 [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。

1. 檢查 R base 和 RevoScaleR 套件的版本，確認現有的版本低於您打算用來取代它們的版本。 

    ```sql
    EXECUTE sp_execute_external_script
    @language=N'R'
    ,@script = N'str(OutputDataSet);
    packagematrix <- installed.packages();
    Name <- packagematrix[,1];
    Version <- packagematrix[,3];
    OutputDataSet <- data.frame(Name, Version);'
    , @input_data_1 = N''
    WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
    ```

1. 關閉 SSMS 和目前與 SQL Server 連線的任何其他工具。 繫結會覆寫程式檔案。 如果 SQL Server 有已開啟的工作階段，繫結將會失敗，並顯示繫結錯誤碼 6。

1. 將 Microsoft Machine Learning Server 下載到您要升級執行個體的電腦上。 我們建議使用[最新版本](/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer) \(英文\)。

1. 將資料夾解壓縮並啟動位於 MLSWIN93 之下的 ServerSetup.exe。

1. 在 [設定安裝] 上，確認要升級的元件，並檢閱相容執行個體的清單。

1. 在 [授權合約] 頁面上，選取 [我接受這些條款] 以接受 Machine Learning Server 的授權條款。 

1. 在後續頁面上，同意您所選取的任何開放原始碼元件 (例如 Microsoft R Open 或 Python Anaconda 散發) 的其他授權條件。

1. 在 [就快完成了] 頁面上，記下安裝資料夾。 預設資料夾為 \Program Files\Microsoft\ML Server。

    如果您想要變更安裝資料夾，請選取 [進階] 以返回精靈的第一頁。 不過，您必須重複所有先前的選取項目。

如果升級失敗，請檢查 [SqlBindR 錯誤碼](#sqlbindr-error-codes) 以取得詳細資訊。

## <a name="offline-binding-no-internet-access"></a>離線繫結 (無法存取網際網路)

對於沒有網際網路連線的系統，您可以將安裝程式和 .cab 檔案下載到連線到網際網路的電腦，然後將檔案傳輸到隔離的伺服器。

安裝程式 (ServerSetup.exe) 包含 Microsoft 套件 (RevoScaleR、MicrosoftML、olapR、sqlRUtils)。 .cab 檔案提供其他核心元件。 例如，"SRO" cab 提供 R Open，這是 Microsoft 的開放原始碼 R 散發。

下列指示說明如何放置檔案以進行離線安裝。

1. 下載 MLSWIN93 安裝程式。 它會以單一壓縮檔案的形式下載。 我們建議您使用[最新版本](/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)，但是您也可以安裝[舊版](/machine-learning-server/install/r-server-install-windows-offline#download-required-components)。

1. 下載 .cab 檔案。 下列連結適用於 9.3 版本。 如果您需要舊版，可以在 [R Server 9.1](/machine-learning-server/install/r-server-install-windows-offline#download-required-components) 中找到其他連結。 回想一下，您只能將 Python/Anaconda 新增至 SQL Server 機器學習服務執行個體。 Python 與 R 都存在預先定型模型；.cab 會以您所使用的語言提供模型。

    | 功能 | 下載 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 預先定型的模型 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. 將 .zip 和 .cab 檔案傳送到目標伺服器。

1. 在伺服器上，於 [執行] 命令中輸入 `%temp%`，以取得暫存目錄的實體位置。 實體路徑因機器而異，但通常是 `C:\Users\<your-user-name>\AppData\Local\Temp`。

1. 將 .cab 檔案放在 %temp% 資料夾中。

1. 解壓縮安裝程式。

1. 執行 ServerSetup.exe 並遵循螢幕上的提示來完成安裝。

## <a name="command-line-operations"></a><a name="bkmk_BindCmd"></a>命令列作業


> [!TIP]
> 找不到 SqlBindR 嗎？ 您可能未執行安裝程式。
> 只有在執行 Machine Learning Server 安裝程式之後，才能使用 SqlBindR。

1. 以系統管理員身分開啟命令提示字元，並瀏覽至包含 sqlbindr.exe 的資料夾。 預設位置是 C:\Program Files\Microsoft\MLServer\Setup

2. 輸入下列命令以檢視可用的執行個體清單︰ `SqlBindR.exe /list`
  
   請記下列出的完整執行個體名稱。 例如，針對預設執行個體，執行個體名稱可能是 MSSQL14.MSSQLSERVER，或類似 SERVERNAME.MYNAMEDINSTANCE 的名稱。

3. 搭配 */bind* 引數執行 **SqlBindR.exe** 命令。 使用上一個步驟中所傳回的執行個體名稱指定要升級的執行個體名稱。

   例如，若要升級預設執行個體，請輸入：`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 當升級完成後，請重新啟動與任何已修改的執行個體相關的啟動控制板服務。

## <a name="revert-or-unbind-an-instance"></a><a name="bkmk_Unbind"></a>還原或解除繫結執行個體

您可以將繫結的執行個體還原到 Python 和 R 元件的初始安裝 (由 SQL Server 安裝程式建立)。 還原回 SQL Server 服務的過程分為三個部分。

+ [步驟 1：從 Microsoft Machine Learning Server 解除繫結](#step-1-unbind)
+ [步驟 2：將執行個體還原為原始狀態](#step-2-restore)
+ [步驟 3：重新安裝您新增至安裝的任何套件](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>步驟 1:解除繫結

您有兩個復原繫結的選項：重新執行安裝程式，或使用 SqlBindR 命令列公用程式。

#### <a name="unbind-using-setup"></a><a name="bkmk_wizunbind"></a> 使用安裝程式解除繫結

1. 找出 Machine Learning Server 的安裝程式。 如果您已移除安裝程式，則可能需要再次下載，或從另一部電腦加以複製。
2. 請務必在具有要解除繫結之執行個體的電腦上執行安裝程式。
2. 安裝程式會識別用於解除繫結之候選項目的本機執行個體。
3. 取消選取您想要還原為原始設定之執行個體旁的核取方塊。
4. 接受所有授權合約。
5. 選取 [完成]。 該程序需要一段時間。

#### <a name="unbind-using-the-command-line"></a><a name="bkmk_cmdunbind"></a> 使用命令列解除繫結

1. 開啟命令提示字元並瀏覽至包含 **sqlbindr.exe** 的資料夾，如上一節所述。

2. 搭配 */unbind* 引數執行 **SqlBindR.exe** 命令，並指定執行個體。

   例如，以下命令列會還原預設執行個體：
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>步驟 2:修復 SQL Server 執行個體

執行 SQL Server 安裝程式，以修復具有 Python 和 R 功能的資料庫引擎執行個體。 已經存在的更新會予以保留。 如果 Python 和 R 套件的維護更新遺漏更新，則適用下一個步驟。

替代解決方案：完全解除安裝並重新安裝資料庫引擎執行個體，然後套用所有服務更新。

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>步驟 3：新增任何協力廠商套件

您可能已將其他開放原始碼或協力廠商套件新增至您的套件程式庫。 由於反轉繫結會切換預設套件程式庫的位置，因此必須將套件重新安裝至 Python 和 R 現在使用的程式庫中。 如需詳細資訊，請參閱 [R 套件資訊](../package-management/r-package-information.md)和[安裝](../package-management/install-additional-r-packages-on-sql-server.md)，以及 [Python 套件資訊](../package-management/python-package-information.md)和[安裝](../package-management/install-additional-python-packages-on-sql-server.md)。

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR.exe 命令語法

### <a name="usage"></a>使用量

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>參數

|名稱|描述|
|------|------|
|list| 顯示目前電腦上所有 SQL Server 執行個體識別碼的清單|
|*bind*| 將指定的 SQL Server 執行個體升級到最新版 R Server，並確保執行個體自動取得 R Server 的未來升級|
|*unbind*|將最新版 R Server 從指定的 SQL Server 執行個體解除安裝，並防止未來的 R Server 升級影響執行個體|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>繫結錯誤

Machine Learning Server 安裝程式和 SqlBindR 都會傳回下列錯誤碼和訊息。

|錯誤碼  | 訊息           | 詳細資料               |
|------------|-------------------|-----------------------|
|繫結錯誤 0 | 確定 (成功) | 已傳遞繫結，但沒有任何錯誤。 |
|繫結錯誤 1 | 無效的引數 | 語法錯誤。 |
|繫結錯誤 2 | 無效的動作 | 語法錯誤。 |
|繫結錯誤 3 | 無效的執行個體 | 執行個體存在，但對繫結而言無效。 |
|繫結錯誤 4 | 不可繫結 | |
|繫結錯誤 5 | 已繫結 | 您執行了 *bind* 命令，但指定的執行個體已經繫結。 |
|繫結錯誤 6 | 繫結失敗 | 解除繫結執行個體時發生錯誤。 如果您執行 Machine Learning Server 安裝程式，但未選取任何功能，就會發生此錯誤。 繫結需要您同時選取 MSSQL 執行個體與 Python 和 R (假設執行個體是 SQL Server 2017)。 如果 SqlBindR 無法寫入 [Program Files] 資料夾，也會發生此錯誤。 開啟工作階段或 SQL Server 的控制代碼會導致此錯誤發生。 如果您收到此錯誤，請在啟動任何新的工作階段之前，將電腦重新開機並重做繫結步驟。|
|繫結錯誤 7 | 未繫結 | 資料庫引擎執行個體具有 R Services 或 SQL Server 機器學習服務。 執行個體未繫結至 Microsoft Machine Learning Server。 |
|繫結錯誤 8 | 解除繫結失敗 | 解除繫結執行個體時發生錯誤。 |
|繫結錯誤 9 | 找不到任何執行個體 | 在這部電腦上找不到任何資料庫引擎執行個體。 |

## <a name="known-issues"></a>已知問題

本節列出使用 SqlBindR.exe 公用程式的特定已知問題，或可能會影響 SQL Server 執行個體之 Machine Learning Server 升級的已知問題。

### <a name="restoring-packages-that-were-previously-installed"></a>還原先前安裝的套件

SqlBindR.exe 無法藉由升級至 Microsoft R Server 9.0.1 來還原原始套件或 R 元件。 在執行個體上使用 SQL Server 修復，並套用所有服務版本。 重新啟動執行個體。

較新的 SqlBindR 版本會自動還原 R 原始功能，而不需要重新安裝 R 元件或重新修補伺服器。 不過，您必須安裝在初始安裝之後可能已新增的任何 R 套件更新。

使用 R 命令使用資料庫中的記錄將已安裝的套件同步處理到檔案系統。 如需詳細資訊，請參閱 [SQL Server 的 R 套件管理](../package-management/install-additional-r-packages-on-sql-server.md)。

### <a name="problems-with-overwritten-sqlbinrini-file-in-sql-server"></a>SQL Server 中遭覆寫之 sqlbinr.ini 檔案的問題

案例：將 Machine Learning Server 9.4.7 繫結到 SQL Server 2017 時，會發生此問題。  更新並繫結 Python 時，或當您更新到新的 CU 時，其不會了解 Python 已繫結，因此會覆寫檔案。 R 沒有已知問題。

因應措施是在非空 PYTHON_SERVICES 目錄中建立 `sqlbindr.ini` 檔案。 內容不會影響檔案的運作方式。

建立包含 **9.4.7.82** 的 `sqlbindr.ini` 檔案，並儲存到此位置：  

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>從 SQL Server 進行多重升級的問題

案例：先前已升級到 9.0.1 的 SQL Server 2016 R Services 執行個體。 已針對 Microsoft R Server 9.1.0 執行新安裝程式。 安裝程式顯示所有有效執行個體的清單。
根據預設，安裝程式會選取先前繫結的執行個體。 如果繼續，先前繫結的執行個體會解除繫結。 結果是會移除先前的 9.0.1 安裝，除了安裝新版 Microsoft R Server (9.1.0)，任何相關套件都未安裝。

因應措施是修改現有的 R Server 安裝，如下所示：
1. 在 [控制台] 中，開啟 [新增或移除程式]。
2. 找到 Microsoft R Server，然後選取 [變更/修改]。
3. 當安裝程式啟動時，請選取您想要繫結至 9.1.0 的執行個體。

Microsoft Machine Learning Server 9.2.1 和 9.3 不會有這個問題。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>繫結或解除繫結會保留多個暫存資料夾

安裝完成後請移除暫存資料夾。

> [!NOTE]
> 請務必等到安裝完成。 移除與某個版本相關聯的 R 程式庫，然後再加入新的 R 程式庫可能需要很長時間。 當作業完成時，就會移除暫存資料夾。

## <a name="see-also"></a>另請參閱

+ [變更預設的 R 或 Python 語言執行階段版本](./change-default-language-runtime-version.md)
+ [安裝適用於 Windows 的 Machine Learning Server (已連線到網際網路)](/machine-learning-server/install/machine-learning-server-windows-install)
+ [安裝適用於 Windows 的 Machine Learning Server (離線)](/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Machine Learning Server 中的已知問題](/machine-learning-server/resources-known-issues)
+ [舊版 R Server 的功能公告](/r-server/whats-new-in-r-server)
+ [已淘汰，不再支援或變更功能](/machine-learning-server/resources-deprecated-features) \(英文\)