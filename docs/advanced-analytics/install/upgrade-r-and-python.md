---
title: 升級 R 和 Python 元件
description: 在 SQL Server 2016 服務或 SQL Server 2017 Machine Learning 服務中升級 R 和 Python, 並使用 sqlbindr 來系結至 Machine Learning Server。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: def007433075920e419f0bf77be5977d1145f793
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344955"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>升級 SQL Server 實例中的機器學習 (R 和 Python) 元件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 中的 R 和 Python 整合包含開放原始碼和 Microsoft 專屬的套件。 在 [標準 SQL Server 服務] 底下, 會根據 SQL Server 發行週期更新套件, 並針對目前版本的現有封裝進行 bug 修正, 但不升級主要版本。 

不過, 許多資料科學家都習慣使用較新的套件, 因為它們可供使用。 針對 SQL Server 2017 Machine Learning 服務 (資料庫內) 和 SQL Server 2016 R Services (資料庫內), 您可以藉由系結至**Microsoft Machine Learning Server**來取得[較新版本的 R 和 Python](#version-map) 。  

## <a name="what-is-binding"></a>什麼是系結？

系結是一種安裝程式, 會將 R_SERVICES 和 PYTHON_SERVICES 資料夾的內容與[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)中的較新可執行檔、程式庫和工具交換。

隨著更新的元件, 在服務模型中會有一個參數。 您的服務更新現在符合[Microsoft R Server 的支援時程表 & Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)在[現代化生命週期](https://support.microsoft.com/help/30881/modern-lifecycle-policy)中, 而不是[SQL Server 產品生命週期](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017), [SQL Server 累計更新](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions)。

除了元件版本和服務更新以外, 系結不會變更安裝的基本概念:R 和 Python 整合仍然是 database engine 實例的一部分, 授權不變 (與系結沒有任何額外的成本), 而且 SQL Server 支援原則仍然保留給資料庫引擎。 本文的其餘部分將說明系結機制, 以及它如何適用于每個版本的 SQL Server。

> [!NOTE]
> 系結僅適用于系結至 SQL Server 實例的 (資料庫內) 實例。 系結與 (獨立式) 安裝無關。

**SQL Server 2017 系結考慮**

針對 SQL Server 2017 Machine Learning 服務, 您只需要在 Microsoft Machine Learning Server 開始提供其他套件或較新版本的現有專案時, 才考慮系結。

**SQL Server 2016 系結考慮**

針對 SQL Server 2016 R Services 客戶, 系結會提供已更新的 R 套件、不屬於原始安裝 ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)) 的新套件, 以及[預先定型模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models), 這些都可以在每個新的主要和次要版本上進一步重新整理。[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)。 系結不會提供 Python 支援, 這是 SQL Server 2017 功能。 

<a name="version-map"></a>

## <a name="version-map"></a>版本對應

下表是版本對應, 顯示跨發行車輛的套件版本, 讓您可以在從開始新增 Python 支援之前, 將系結至 Microsoft Machine Learning Server (先前稱為 R 伺服器) 時, 確定可能的升級路徑在 MLS 9.2.1 中)。 

請注意, 系結不保證 R 或 Anaconda 的最新版本。 當您系結至 Microsoft Machine Learning Server (MLS) 時, 您會取得透過安裝程式安裝的 R 或 Python 版本, 這可能不是 web 上可用的最新版本。

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

元件 |初始版本 | [R Server 9.0。1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R 伺服器9。1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
透過 R 的 Microsoft R Open (MRO) | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| 馬丁 | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[預先定型模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| 馬丁 | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 馬丁 | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 馬丁 | 1.0 |  1.0 |  1.0 |  1.0 |


[**SQL Server 2017 Machine Learning 服務**](../install/sql-machine-learning-services-windows-install.md)

元件 |初始版本 | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
透過 R 的 Microsoft R Open (MRO) | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Python 3.5 上的 Anaconda 4。2  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[預先定型模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>元件升級的運作方式 

當您將現有的 R 和 Python 安裝系結至 Machine Learning Server 時, R 和 Python 程式庫和可執行檔會進行升級。 當您在現有的 SQL Server database engine 實例 (2016 或 2017) 上執行安裝程式時, [Microsoft Machine Learning Server 安裝程式](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)會執行系結, 其中包含 R 或 Python 整合。 安裝程式會偵測現有的功能, 並提示您重新系結至 Machine Learning Server。 

在系結期間, C:\Program Files\Microsoft SQL Server\MSSQL14. 的內容MSSQLSERVER\R_SERVICES 和 \PYTHON_SERVICES 會以 C:\Program Files\Microsoft\ML Server\R_SERVER 和 \PYTHON_SERVER. 的較新可執行檔和程式庫覆寫

同時, 服務模型也會從 SQL Server 的更新機制翻轉到較頻繁的 Microsoft Machine Learning Server 主要和次要發行週期。 針對需要較新的層代 R 和 Python 模組作為解決方案的資料科學小組而言, 切換支援原則是個不錯的選項。 

+ 如果沒有系結, 則當您安裝 SQL Server Service Pack 或累積更新 (CU) 時, R 和 Python 套件會針對 bug 修正進行修補。 
+ 使用系結時, 較新的套件版本可在[現代化的生命週期原則](https://support.microsoft.com/help/30881/modern-lifecycle-policy)和 Microsoft Machine Learning Server 的版本之下, 獨立于 CU 發行排程的情況下套用至您的實例。 現代化生命週期支援原則提供更頻繁的較短一年期更新。 後置系結之後, 您會繼續使用 MLS 安裝程式, 以供日後更新 R 和 Python, 因為它們可在 Microsoft 下載網站上取得。

Binding 僅適用于 R 和 Python 功能。 也就是 R 和 Python 功能的開放原始碼套件 (Microsoft R Open、Anaconda), 以及專屬套件 RevoScaleR、revoscalepy 等等。 系結不會變更 database engine 實例的支援模型, 也不會變更 SQL Server 的版本。

可還原系結。 您可以藉由解除系結[實例](#bkmk_Unbind)並 reparing SQL Server 的資料庫引擎實例, 來還原為 SQL Server 服務。

總結, 系結的步驟如下所示:

+ 從現有的已設定安裝的 SQL Server 2016 R Services (或 SQL Server 2017 Machine Learning Services) 開始。
+ 判斷哪個版本的 Microsoft Machine Learning Server 有您想要使用的升級元件。
+ 下載並執行該版本的安裝程式。 安裝程式會偵測現有的實例、加入系結選項, 並傳回相容的實例清單。
+ 選擇您想要系結的實例, 然後完成安裝程式以執行系結。

就使用者經驗而言, 技術及其使用方式不變。 唯一的差別在於是否有較新版本的套件, 以及可能原本無法透過 SQL Server 取得的其他套件 (例如, MicrosoftML for SQL Server 2016 R Services 客戶)。

## <a name="bkmk_BindWizard"></a>使用安裝程式系結至 MLS

Microsoft Machine Learning 安裝程式會偵測現有的功能和 SQL Server 版本, 並叫用名為 SqlBindR 的公用程式來變更系結。 就內部而言, SqlBindR 會連結至設定並間接使用。 之後, 您可以直接從命令列呼叫 SqlBindR, 以執行特定的選項。

1. 在 SSMS 中, `SELECT @@version`執行以確認伺服器符合最低組建需求。 

   針對 SQL Server 2016 R 服務, 最小值為[Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276)和[CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。

1. 檢查 R base 和 RevoScaleR 套件的版本, 確認現有的版本低於您打算用來取代它們的版本。 針對 SQL Server 2016 R 服務, R 基底套件為 3.2.2, 而 RevoScaleR 為8.0.3 版。

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

1. 關閉 SSMS 和任何其他已開啟連接 SQL Server 的工具。 Binding 會覆寫程式檔案。 如果 SQL Server 有已開啟的會話, 系結將會失敗, 並出現 binding 錯誤碼6。

1. 將 Microsoft Machine Learning Server 下載到具有您想要升級之實例的電腦上。 我們建議[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)。

1. 將資料夾解壓縮並啟動 ServerSetup, 其位於 MLSWIN93 之下。

   ![Microsoft Machine Learning Server 安裝程式嚮導](media/mls-921-installer-start.PNG)

1. 在 **[設定安裝**] 上, 確認要升級的元件, 並檢查相容的實例清單。 

   這個步驟非常重要。

   在左側, 選擇您想要保留或升級的每項功能。 您無法升級某些功能, 而不是其他功能。 空白的核取方塊會移除該功能 (假設目前已安裝)。 在螢幕擷取畫面中, 指定了 SQL Server 2016 R Services (MSSQL13.MSSQLSERVER)、R 和 R 版本的預先定型模型的實例。 此設定有效, 因為 SQL Server 2016 支援 R, 但不支援 Python。

   如果您要升級 SQL Server 2016 R 服務上的元件, 請勿選取 [Python] 功能。 您無法將 Python 新增至 SQL Server 2016 R 服務。

   在右側, 選取實例名稱旁邊的核取方塊。 如果沒有列出任何實例, 您就會有不相容的組合。 如果您未選取實例, 就會建立 Machine Learning Server 的新獨立安裝, 而 SQL Server 程式庫則不會變更。 如果您無法選取實例, 它可能不是在[SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。 

    ![設定安裝步驟](media/mls-931-installer-mssql13.png)

1. 在 [**授權合約**] 頁面上, 選取 [**我接受這些條款**] 以接受 Machine Learning Server 的授權條款。 

1. 在後續的頁面上, 為您所選取的任何開放原始碼元件 (例如 Microsoft R Open 或 Python Anaconda 散發), 同意其他授權條件。

1. 在 [**幾乎**] 頁面上, 記下安裝資料夾。 預設資料夾為 \Program Files\Microsoft\ML Server。

    如果您想要變更安裝資料夾, 請按一下 [ **Advanced** ] 返回嚮導的第一頁。 不過, 您必須重複所有先前的選取專案。

在安裝過程中, 會取代 SQL Server 所使用的任何 R 或 Python 程式庫, 並更新啟動列以使用較新的元件。 因此, 如果實例先前使用預設 R_SERVICES 資料夾中的程式庫, 則在升級之後, 會移除這些程式庫, 並將啟動列服務的屬性變更為使用新位置中的程式庫。

系結會影響這些資料夾的內容:C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library 已取代為 C:\Program Files\Microsoft\ML Server\R_SERVER. 的內容 第二個資料夾和其內容是由 Microsoft Machine Learning Server 安裝程式所建立。 

如果升級失敗, 請檢查[SqlBindR 錯誤碼](#sqlbindr-error-codes)以取得詳細資訊。

## <a name="confirm-binding"></a>確認系結

重新檢查 R 和 RevoScaleR 的版本, 確認您有較新的版本。 使用與資料庫引擎實例中的 R 封裝一起散發的 R 主控台來取得封裝資訊:

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

針對系結至 Machine Learning Server 9.3 的 SQL Server 2016 R 服務, R 基底套件應為 3.4.3, RevoScaleR 應為 9.3, 而且您也應該具有 MicrosoftML 9.3。 

如果您已加入預先定型的模型, 模型就會內嵌在 MicrosoftML 程式庫中, 而您可以透過 MicrosoftML 函數來呼叫它們。 如需詳細資訊, 請參閱[適用于 MicrosoftML 的 R 範例](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)。

## <a name="offline-binding-no-internet-access"></a>離線系結 (無法存取網際網路)

對於沒有網際網路連線的系統, 您可以將安裝程式和 .cab 檔案下載到連線到網際網路的電腦, 然後將檔案傳輸到隔離的伺服器。 

安裝程式 (ServerSetup) 包含 Microsoft 套件 (RevoScaleR、MicrosoftML、olapR、sqlRUtils)。 .Cab 檔案提供其他核心元件。 例如, "SRO" cab 提供 R Open、Microsoft 的開放原始碼 R 散發。

下列指示說明如何放置檔案以進行離線安裝。

1. 下載 MLS 安裝程式。 它會以單一壓縮檔案的形式下載。 我們建議[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), 但您也可以安裝[較早](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)的版本。

1. 下載 .cab 檔案。 下列連結適用于9.3 版本。 如果您需要較舊的版本, 可以在[R 伺服器 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)中找到其他連結。 回想一下, 您只能將 Python/Anaconda 新增至 SQL Server 2017 Machine Learning 服務實例。 適用于 R 和 Python 的預先定型模型存在;.cab 會以您所使用的語言提供模型。

    | 功能 | 下載 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 預先定型的模型 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. 將 .zip 和 .cab 檔案傳送到目標伺服器。

1. 在伺服器上, 于`%temp%` [執行] 命令中輸入, 以取得臨時目錄的實體位置。 實體路徑因電腦而異, 但通常`C:\Users\<your-user-name>\AppData\Local\Temp`是。

1. 將 .cab 檔案放在% temp% 資料夾中。

1. 解壓縮安裝程式。

1. 執行 ServerSetup, 並遵循螢幕上的提示來完成安裝。

## <a name="bkmk_BindCmd"></a>命令列作業

執行 Microsoft Machine Learning Server 之後, 就可以使用稱為 SqlBindR 的命令列公用程式, 供您用於進一步的系結作業。 例如, 如果您決定要反轉系結, 您可以重新執行安裝程式或使用命令列公用程式。 此外, 您可以使用此工具來檢查實例相容性和可用性。

> [!TIP]
> 找不到 SqlBindR 嗎？ 您可能未執行安裝程式。 只有在執行 Machine Learning Server 安裝程式之後, 才能使用 SqlBindR。

1. 以系統管理員身分開啟命令提示字元，並瀏覽至包含 sqlbindr.exe 的資料夾。 預設位置為 C:\Program Files\Microsoft\MLServer\Setup

2. 輸入下列命令以檢視可用的執行個體清單︰ `SqlBindR.exe /list`
  
   請記下列出的完整執行個體名稱。 例如, 實例名稱可能是 MSSQL14.。預設實例的 MSSQLSERVER, 或類似 SERVERNAME 的專案。MYNAMEDINSTANCE.

3. 執行**SqlBindR**和 */bind*引數, 並使用上一個步驟中傳回的實例名稱指定要升級之實例的名稱。

   例如, 若要升級預設實例, 請輸入:`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 當升級完成時, 請重新開機與任何已修改之實例相關聯的啟動列服務。

## <a name="bkmk_Unbind"></a>還原或解除系結實例

您可以將系結的實例還原到 R 和 Python 元件的初始安裝 (由 SQL Server 安裝程式建立)。 有三個部分可還原回 SQL Server 服務。

+ [步驟 1：從 Microsoft Machine Learning Server 解除系結](#step-1-unbind)
+ [步驟 2：將實例還原為原始狀態](#step-2-restore)
+ [步驟 3：重新安裝您新增至安裝的任何套件](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>步驟 1：解除系結

您有兩個復原系結的選項: 重新執行安裝程式, 或使用 SqlBindR 命令列公用程式。

#### <a name="bkmk_wizunbind"></a>使用安裝程式解除系結

1. 找出 Machine Learning Server 的安裝程式。 如果您已移除安裝程式, 則可能需要再次下載, 或從另一部電腦複製它。
2. 請務必在具有您要解除系結之實例的電腦上執行安裝程式。
2. 安裝程式會識別屬於用於解除系結之候選的本機實例。
3. 取消選取您想要還原為原始設定之實例旁的核取方塊。
4. 接受授權合約。 即使在安裝時, 您也必須表示您接受授權條款。
5. 按一下 [ **完成**]。 進程需要一段時間。

#### <a name="bkmk_cmdunbind"></a>使用命令列解除系結

1. 開啟命令提示字元並瀏覽至包含 **sqlbindr.exe** 的資料夾，如上一節所述。

2. 搭配 */unbind* 引數執行 **SqlBindR.exe** 命令，並指定執行個體。

   例如, 下列命令會還原預設實例:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>步驟 2：修復 SQL Server 實例

執行 SQL Server 安裝程式, 以修復具有 R 和 Python 功能的 database engine 實例。 系統會保留現有的更新, 但如果您錯過 R 和 Python 套件的任何 SQL Server 服務更新, 此步驟會套用這些修補程式。

或者, 這是更多工具, 但您也可以完全卸載並重新安裝 database engine 實例, 然後套用所有服務更新。

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>步驟 3：新增任何協力廠商套件

您可能已將其他開放原始碼或協力廠商套件新增至您的套件程式庫。 由於反轉系結會切換預設封裝程式庫的位置, 因此您必須將套件重新安裝至 R 和 Python 現在使用的程式庫。 如需詳細資訊, 請參閱[預設封裝](../package-management/default-packages.md)、[安裝新的 R 套件](../r/install-additional-r-packages-on-sql-server.md)和[安裝新的 Python 套件](../python/install-additional-python-packages-on-sql-server.md)。

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR .exe 命令語法

### <a name="usage"></a>使用量

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>參數

|名稱|描述|
|------|------|
|*list*| 顯示目前電腦上所有 SQL 資料庫執行個體識別碼的清單|
|*bind*| 將指定的 SQL 資料庫執行個體升級到最新版 R Server，並確保執行個體自動取得 R Server 的未來升級|
|*unbind*|從指定的 SQL 資料庫執行個體解除安裝最新版的 R Server，並防止未來的 R Server 升級影響執行個體|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>系結錯誤

MLS 安裝程式和 SqlBindR 都會傳回下列錯誤碼和訊息。

|錯誤碼  | Message           | 詳細資料               |
|------------|-------------------|-----------------------|
|系結錯誤0 | 確定 (成功) | 已傳遞系結, 但沒有任何錯誤。 |
|系結錯誤1 | 不正確引數 | 語法錯誤。 |
|系結錯誤2 | 不正確動作 | 語法錯誤。 |
|系結錯誤3 | 不正確實例 | 實例存在, 但對系結而言是不正確。 |
|系結錯誤4 | 不可系結 | |
|Bind 錯誤5 | 已系結 | 您執行了 *bind* 命令，但指定的執行個體已經繫結。 |
|系結錯誤6 | 系結失敗 | 解除系結實例時發生錯誤。 如果您執行 MLS 安裝程式, 但未選取任何功能, 就會發生此錯誤。 系結需要您同時選取 MSSQL 實例和 R 和 Python, 假設實例是 SQL Server 2017。 如果 SqlBindR 無法寫入 Program Files 資料夾, 也會發生此錯誤。 開啟會話或 SQL Server 的控制碼會導致此錯誤發生。 如果您收到此錯誤, 請先重新開機電腦, 然後重做系結步驟, 再開始任何新的會話。|
|系結錯誤7 | 未系結 | 資料庫引擎實例具有 R 服務或 SQL Server Machine Learning 服務。 實例未系結至 Microsoft Machine Learning Server。 |
|Bind 錯誤8 | 解除系結失敗 | 解除系結實例時發生錯誤。 |
|系結錯誤9 | 找不到任何執行個體 | 在這部電腦上找不到任何資料庫引擎實例。 |

## <a name="known-issues"></a>已知問題

本節列出使用 SqlBindR 公用程式的特定已知問題, 或升級可能會影響 SQL Server 實例的 Machine Learning Server。

### <a name="restoring-packages-that-were-previously-installed"></a>還原先前安裝的封裝

如果您升級至 Microsoft R Server 9.0.1, 該版本的 SqlBindR 版本無法完全還原原始封裝或 R 元件, 要求使用者在實例上執行 SQL Server 修復, 套用所有服務版本, 然後重新開機實例。

較新版本的 SqlBindR 會自動還原原始 R 功能, 而不需要重新安裝 R 元件或重新修補伺服器。 不過, 您必須安裝在初始安裝之後可能已新增的任何 R 套件更新。

如果您已使用套件管理角色來安裝和共用封裝, 此工作會變得更容易: 您可以使用 R 命令, 將已安裝的封裝同步處理到使用資料庫中記錄的檔案系統, 反之亦然。 如需詳細資訊, 請參閱[SQL Server 的 R 封裝管理](../r/install-additional-r-packages-on-sql-server.md)。

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>從 SQL Server 進行多重升級的問題

如果您先前已將 SQL Server 2016 R 服務的實例升級至 9.0.1, 當您執行 Microsoft R Server 9.1.0 的新安裝程式時, 它會顯示所有有效實例的清單, 然後依預設選取先前系結的實例。 如果繼續, 先前系結的實例會解除系結。 如此一來, 就會移除先前的9.0.1 安裝, 包括任何相關的套件, 但不會安裝新版的 Microsoft R Server (9.1.0)。

因應措施是修改現有的 R 伺服器安裝, 如下所示:
1. 在 [控制台] 中, 開啟 [**新增或移除程式**]。
2. 找出 [Microsoft R Server], 然後按一下 [**變更/修改**]。
3. 當安裝程式啟動時, 請選取您想要系結至9.1.0 的實例。

Microsoft Machine Learning Server 9.2.1 和9.3 不會有這個問題。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>系結或解除系結會保留多個暫存資料夾

有時系結和解除系結作業無法清除暫存資料夾。
如果您找到名稱類似的資料夾, 您可以在安裝完成後將其移除:R_SERVICES_<guid>

> [!NOTE]
> 請務必等到安裝完成。 可能需要很長的時間來移除與某個版本相關聯的 R 程式庫, 然後再加入新的 R 程式庫。 當作業完成時, 就會移除暫存資料夾。

## <a name="see-also"></a>另請參閱

+ [安裝適用于 Windows 的 Machine Learning Server (已連線到網際網路)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [安裝適用于 Windows 的 Machine Learning Server (離線)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Machine Learning Server 中的已知問題](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [舊版 R Server 的功能公告](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [已淘汰、已停止或已變更的功能](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
