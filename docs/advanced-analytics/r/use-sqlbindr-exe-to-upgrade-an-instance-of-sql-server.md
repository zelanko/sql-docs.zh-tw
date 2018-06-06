---
title: 升級 SQL Server R 執行個體 （機器學習服務） 中的 R，並將 Python 元件 |Microsoft 文件
description: 升級 R 和 SQL Server 2016 R Services 或 SQL Server 2017 機器學習服務繫結到機器學習伺服器使用 sqlbindr.exe Python。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 11b9e58c583712d8ee5ae70f4dbb98b6c175239c
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707686"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>升級 SQL Server 執行個體中的機器學習 （R 和 Python） 元件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 中的 R，並將 Python 整合包括開放原始碼和 Microsoft 專屬封裝。 在標準的 SQL Server 服務，R，並將 Python 封裝會根據 SQL Server 發行週期內，其中修正了錯誤，目前版本的現有套件更新。 

大部分的資料科學家習慣使用較新的封裝，當它們變成可用。 SQL Server 2017 機器學習服務 （資料庫） 和 SQL Server 2016 R Services （資料庫） 中，您可以取得較新版本的 R，並將 Python 藉由變更*繫結*從 SQL Server 服務至[Microsoft機器學習伺服器](https://docs.microsoft.com/en-us/machine-learning-server/index)和[現代的生命週期支援原則](https://support.microsoft.com/help/30881/modern-lifecycle-policy)。

繫結不會變更您的安裝的基本概念： R，並將 Python 整合仍然是一部分的資料庫引擎執行個體中，授權會維持不變的 （不需要其他成本與繫結相關聯），而且 SQL Server 支援原則仍保留資料庫引擎。 但是重新繫結將 R，並將 Python 封裝服務的方式。 本文的其餘部分說明繫結機制，以及每個版本的 SQL Server 的運作方式。

> [!NOTE]
> 繫結 （資料庫） 執行個體只會套用。 繫結 （獨立） 安裝無關。

**SQL Server 2017 繫結的考量**

SQL Server 2017 機器學習服務，您可以在 Microsoft Machine Learning 伺服器會開始提供額外的套件，或已經有透過您的較新版本時，才考慮繫結。

**SQL Server 2016 繫結的考量**

SQL Server 2016 R 服務繫結的客戶提供更新的 R 封裝，新的封裝不屬於預先定型的模型，全部都是可進一步重新整理每個新的主要和次要版本的 Microsoft Machine Learning 伺服器在與原始安裝的一部分。 繫結並不會提供 Python 支援，這是 SQL Server 2017 功能。 

## <a name="version-map"></a>版本的對應

下表是版本對應，跨版本車輛顯示封裝版本，如此當您繫結至 Microsoft 機器學習 Server （先前稱為 R Server 的 Python 支援加法之前，您可以確定 potentional 升級路徑MLS 9.2.1 中起始）。 

請注意繫結並不保證 R 或 Anaconda 的最新版本。 當您繫結至 Microsoft 機器學習伺服器 (MLS) 時，您會取得安裝程式可能不會在網站上可用的最新版本的 R 或 Python 版本。

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

元件 |初版 | [R 伺服器 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R 伺服器 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
Microsoft R Open (MRO) 透過 R | R 3.2.2     | R 3.3.2   |3.3.3 R   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[預先定型的模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |


[**SQL Server 2017 機器學習服務**](../install/sql-machine-learning-services-windows-install.md)

元件 |初版 | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
Microsoft R Open (MRO) 透過 R | 3.3.3 R | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
透過 Python 3.5 anaconda 4.2  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[預先定型的模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>元件升級的運作方式

元件升級是透過*繫結*的 SQL Server 2016 R 服務執行個體 （或 SQL Server 2017 機器學習服務執行個體） 到[Microsoft Machine Learning 伺服器](https://docs.microsoft.com/machine-learning-server/index)。 

Microsoft Machine Learning 伺服器是在內部部署伺服器產品分隔來自 SQL Server，但具有相同的解譯器和封裝。 繫結交換出 SQL Server 服務的更新機制，以便您可以使用 R 和 Python 封裝傳送與 Microsoft Machine Learning 伺服器，而這通常是新的 SQL Server 安裝的。 切換支援原則會需要較新的層代 R 資料科學小組的理想選擇和 Python 模組及其解決方案。 

繫結的執行方式[MLS installer](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。 安裝程式會更新特定的 R，並將 Python 封裝，但不會取代您的 SQL Server 資料庫中執行個體與獨立，中斷連接的伺服器安裝。

+ 沒有繫結，R 和 Python 封裝會修補個 bug 修正，當您安裝 SQL Server service pack 或累積更新 (CU)。 
+ 使用繫結，較新的封裝版本可套用至您的執行個體，獨立的 CU 發行排程，底下[現代的生命週期原則](https://support.microsoft.com/help/30881/modern-lifecycle-policy)和版本的 Microsoft Machine Learning 伺服器。 現代的生命週期支援原則會提供更頻繁的更新，比短、 一年的使用期限。 後置繫結，您會繼續使用 R，並將 Python 未來更新在 Microsoft Machine Learning 伺服器可用時 MLS 安裝程式。

繫結適用於 R，並將 Python 功能。 也就是開放原始碼套件的 R，並將 Python 功能 （Microsoft R Open、 Anaconda） 及專屬封裝 RevoScaleR、 revoscalepy，等等。 繫結不會變更支援模型的資料庫引擎執行個體，並不會變更的 SQL Server 版本。

繫結是可復原項目。 您可以還原至 SQL Server 服務由[解除繫結執行個體](#bkmk_Unbind)和 reparing SQL Server database engine 執行個體。

加總，繫結的步驟如下：

+ 使用現有的設定安裝 SQL Server 2016 R 服務 （或 SQL Server 2017 機器學習服務） 啟動。
+ 判斷哪個版本的 Microsoft Machine Learning 伺服器具有您想要使用的升級的元件。
+ 下載並執行該版本的安裝程式。 安裝程式偵測到現有的執行個體，加入繫結 選項，並傳回相容的執行個體的清單。
+ 選擇您想要繫結，然後在完成安裝程式來執行繫結的執行個體。

根據使用者體驗、 技術及如何使用它不會變更。 唯一的差別在於較新版本的封裝和可能的其他封裝原本可透過 SQL Server （例如 SQL Server 2016 R 服務客戶 MicrosoftML)。

## <a name="bkmk_BindWizard"></a>繫結至 MLS 使用安裝程式

Microsoft Machine Learning 安裝程式偵測到現有的功能和 SQL Server 版本，並叫用稱為 SqlBindR.exe 變更繫結的公用程式。 就內部而言，安裝程式進行鏈結 SqlBindR 且間接使用。 稍後，您可以呼叫 SqlBindR 直接從命令列，以執行特定的選項。

1. 在 SSMS 中，執行`SELECT @@version`，確認伺服器符合最低的組建需求。 

   最小值是 SQL Server 2016 R services [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276)和[CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。

1. 請檢查確認現有的版本低於您打算將其取代為 R 基底和 RevoScaleR 封裝版本。 SQL Server 2016 R services R 基底套件是 3.2.2 而 RevoScaleR 8.0.3。

    ```SQL
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

1. 下載 Microsoft Machine Learning 伺服器到具有您想要升級的執行個體的電腦上。 我們建議[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)。

1. 解壓縮的資料夾，並啟動 ServerSetup.exe，位於 MLSWIN93。

   ![Microsoft Machine Learning 伺服器安裝精靈](media/mls-921-installer-start.PNG)

1. 在**設定安裝**，確認要升級，元件，然後檢閱相容的執行個體的清單。 

   在左邊，選擇您想要保留或升級的每一項功能。 您無法升級某些功能並不是其他人。 空的核取方塊中移除該功能，假設目前已安裝的功能。 在螢幕擷取畫面、 執行個體的 SQL Server 2016 R 服務 (MSSQL13)，會選取 R 和預先定型的模型的 R 版本。 此設定是有效的因為 SQL Server 2016 支援 R，但不是 Python 支援。

   在右側，選取執行個體名稱旁的核取方塊。 如果沒有列出任何執行個體，您會有不相容的組合。 如果您未選取執行個體，建立新的獨立安裝的機器學習伺服器時，與 SQL Server 程式庫並不會變更。 如果您無法選取執行個體，它可能無法在[SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。 

    ![Microsoft Machine Learning 伺服器安裝精靈](media/mls-931-installer-mssql13.png)

1. 在**授權合約**頁面上，選取**我接受這些條款**機器學習伺服器接受授權條款。 

1. 在後續頁面中，提供額外的授權條款，選取，例如 Microsoft R Open 或 Python Anaconda 發佈任何開放原始碼元件的同意。

1. 在**幾乎那里**頁面上，記下的安裝資料夾。 預設資料夾是 \Program Files\Microsoft\ML 伺服器。

    如果您想要變更安裝資料夾，按一下**進階**返回精靈的第一頁。 不過，您必須重複先前的所有選項。

在安裝過程中，會取代任何 SQL Server 所使用的 R 或 Python 程式庫，並啟動控制板會更新以使用較新的元件。 如此一來，如果執行個體之前會使用預設 R_SERVICES 資料夾中的程式庫，升級之後移除這些程式庫，並啟動控制板服務的屬性都會變更為使用新的位置中的程式庫。

繫結會影響這些資料夾的內容： C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library 會取代 C:\Program Files\Microsoft\ML Server\R_SERVER 的內容。 Microsoft Machine Learning Server 安裝程式會建立第二個資料夾及其內容。 

如果升級失敗，請檢查[SqlBindR 錯誤碼](#sqlbindr-error-codes)如需詳細資訊。

## <a name="confirm-binding"></a>確認繫結

重新檢查以確認您有較新版本的 R 與 RevoScaleR 的版本。 您可以使用 R 主控台與您的資料庫引擎執行個體中的 R 封裝一起散發，取得封裝資訊：

```SQL
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

繫結至機器學習伺服器 9.3 SQL Server 2016 R 服務，如 R 基底套件能 3.4.1、 RevoScaleR 應 9.3，而且您也應該擁有 MicrosoftML 9.3。 

如果您加入預先定型的模型，模型會內嵌在 MicrosoftML 程式庫，而且您可以透過 MicrosoftML 函式呼叫它們。 如需詳細資訊，請參閱[MicrosoftML R 範例](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)。

## <a name="offline-binding-no-internet-access"></a>離線的繫結 （沒有網際網路存取）

沒有網際網路連線的系統，可以將安裝程式和.cab 檔案下載到連接網際網路的電腦上，並再將檔案傳輸到隔離的伺服器。 

安裝程式 (ServerSetup.exe) 包含 RevoScaleR、 MicrosoftML、 olapR （sqlRUtils） 的 Microsoft 套件。 .Cab 檔案提供其他核心元件。 例如，"SRO"封包提供 R Open，Microsoft 發佈的開放原始碼。

下列指示說明如何進行離線安裝檔案。

1. 下載 MLS 安裝程式。 它會下載成單一的壓縮檔案。 我們建議[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)，但您也可以安裝[舊版](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)。

1. 下載的.cab 檔。 下列連結是 9.3 的版本。 如果您需要更早版本，其他連結位於[R 伺服器 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)。 前文提過 Python/Anaconda 只能加入至 SQL Server 2017 機器學習服務執行個體。 預先定型的模型存在 R 和 Python;.cab 會提供您使用的語言中的模型。

    | 功能 | 下載 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 預先定型的模型 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. .Zip 和.cab 檔案傳送給目標伺服器。

1. 在伺服器上，輸入`%temp%`[執行] 命令，以取得暫存目錄的實體位置中。 實體路徑會因電腦而異，但它通常是`C:\Users\<your-user-name>\AppData\Local\Temp`。

1. 將.cab 檔放在 %temp%資料夾中。

1. 解壓縮安裝程式。

1. 執行 ServerSetup.exe 並遵循螢幕上的提示完成安裝。

## <a name="bkmk_BindCmd"></a>命令列作業

執行 Microsoft Machine Learning 伺服器之後，稱為 SqlBindR.exe 的命令列公用程式會變成可用，您可用於進一步繫結作業。 例如，您應該決定要反轉的繫結，您無法重新執行安裝程式或使用命令列公用程式。 此外，您可以使用此工具來檢查執行個體的相容性和可用性。

> [!TIP]
> 找不到 SqlBindR？ 您可能尚未執行安裝程式。 執行機器學習 Server 安裝程式後，才可 SqlBindR。

1. 以系統管理員身分開啟命令提示字元，並瀏覽至包含 sqlbindr.exe 的資料夾。 預設位置是 C:\Program Files\Microsoft\MLServer\Setup

2. 輸入下列命令以檢視可用的執行個體清單︰ `SqlBindR.exe /list`
  
   請記下列出的完整執行個體名稱。 例如，執行個體名稱可能是 MSSQL14。MSSQLSERVER 是預設執行個體，或伺服器名稱如下的值。已 MYNAMEDINSTANCE。

3. 執行**SqlBindR.exe**命令搭配 */繫結*引數，並指定要升級之執行個體名稱使用上一個步驟中傳回的執行個體名稱。

   例如，若要升級的預設執行個體，請輸入：  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 在升級完成後，請重新啟動任何已修改的執行個體相關聯的啟動控制板服務。

## <a name="bkmk_Unbind"></a>還原或解除繫結執行個體

您可以還原繫結的執行個體到初始安裝 R，並將 Python 元件，SQL Server 安裝程式所建立。 有三個部分還原到 SQL Server 服務。

+ [步驟 1： 解除繫結，從 Microsoft 機器學習服務伺服器](#step-1-unbind)
+ [步驟 2： 將執行個體還原為原始狀態](#step-2-restore)
+ [步驟 3： 重新安裝任何套件新增至安裝](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>步驟 1： 解除繫結

您有兩個復原繫結的選項： 重新執行安裝程式，或使用 SqlBindR 命令列公用程式。

#### <a name="bkmk_wizunbind"></a> 解除繫結使用安裝程式

1. 找出機器學習服務伺服器的安裝程式。 如果您已經移除安裝程式，您可能需要下載一次，或將它複製從另一部電腦。
2. 請務必在具有您想要解除繫結的執行個體的電腦上執行安裝程式。
2. 安裝程式會識別會被解除繫結的本機執行個體。
3. 取消選取您想要還原為原始設定的執行個體旁邊的核取方塊。
4. 接受授權合約。 您必須在安裝時，指出您接受授權條款偶數。
5. 按一下 **[完成]**。 處理程序需要一些時間。

#### <a name="bkmk_cmdunbind"></a> 使用命令列解除繫結

1. 開啟命令提示字元並瀏覽至包含 **sqlbindr.exe** 的資料夾，如上一節所述。

2. 搭配 */unbind* 引數執行 **SqlBindR.exe** 命令，並指定執行個體。

   例如，下列命令會還原預設執行個體：
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>步驟 2： 修復 SQL Server 執行個體

執行 SQL Server 安裝程式修復具有 R，並將 Python 功能的資料庫引擎執行個體。 會保留現有的更新，但如果遺漏任何 SQL Server，服務 R，並將 Python 封裝更新時，這個步驟適用於這些修補檔案。

或者，這是更多工作，但您可能也完全解除安裝和重新安裝 database engine 執行個體，並再將所有的服務更新套用。

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>步驟 3： 加入任何第三方封裝

您可能已經將其他開放原始碼或協力廠商封裝加入您的封裝程式庫。 因為反轉繫結參數的預設套件程式庫的位置，您必須重新安裝現在使用 R，並將 Python 的文件庫的封裝。 如需詳細資訊，請參閱[預設封裝](installing-and-managing-r-packages.md)，[安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)，和[安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)。

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR.exe 命令語法

### <a name="usage"></a>使用方式

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>參數

|[屬性]|描述|
|------|------|
|*list*| 顯示目前電腦上所有 SQL 資料庫執行個體識別碼的清單|
|*bind*| 將指定的 SQL 資料庫執行個體升級到最新版 R Server，並確保執行個體自動取得 R Server 的未來升級|
|*unbind*|從指定的 SQL 資料庫執行個體解除安裝最新版的 R Server，並防止未來的 R Server 升級影響執行個體|

<a name="sqlbinder-error-codes"><a/>

## <a name="binding-errors"></a>繫結錯誤

MLS Installer 和 SqlBindR 會傳回下列錯誤碼和訊息。

|錯誤碼  | 訊息           | 詳細資料               |
|------------|-------------------|-----------------------|
|繫結錯誤 0 | 沒問題 （成功） | 繫結傳遞未發生任何錯誤。 |
|繫結錯誤 1 | 無效的引數 | 語法錯誤。 |
|繫結錯誤 2 | 無效的動作 | 語法錯誤。 |
|繫結錯誤 3 | 無效的執行個體 | 執行個體存在，但不是有效的繫結。 |
|繫結錯誤 4 | 不繫結 | |
|繫結錯誤 5 | 已繫結 | 您執行了 *bind* 命令，但指定的執行個體已經繫結。 |
|繫結錯誤 6 | 繫結失敗 | 解除繫結執行個體時發生錯誤。 如果您執行 MLS 安裝程式，而不選取任何功能，就會發生此錯誤。 繫結會要求您選取 MSSQL 執行個體和 R 和 Python，假定執行個體是 SQL Server 2017。|
|繫結錯誤 7 | 未繫結 | 資料庫引擎執行個體有 R Services 或 SQL Server 機器學習服務。 執行個體未繫結到 Microsoft 機器學習服務伺服器。 |
|繫結錯誤 8 | 解除繫結失敗 | 解除繫結執行個體時發生錯誤。 |
|繫結錯誤 9 | 找不到任何執行個體 | 找不到此電腦上的任何 database engine 執行個體。 |

## <a name="known-issues"></a>已知問題

此區段會列出特有使用 SqlBindR.exe 公用程式，或升級的機器學習伺服器可能會影響 SQL Server 執行個體的已知的問題。

### <a name="restoring-packages-that-were-previously-installed"></a>還原先前安裝的封裝

如果您升級到 Microsoft R Server 9.0.1，該版本 SqlBindR.exe 版本無法還原原始封裝或 R 元件完整地要求使用者執行個體上，執行 SQL Server 修復套用所有的服務版本，然後再重新啟動執行個體。

新版 SqlBindR 自動還原原始的 R 功能，因而不須重新安裝的 R 元件，或重新修補程式的伺服器。 不過，您必須安裝任何可能在初始安裝後加入的 R 封裝更新。

如果您已經使用封裝管理角色來安裝及共用封裝，這項工作就能輕鬆： 您可以使用 R 命令來同步處理已安裝的封裝，在資料庫中，使用記錄在檔案系統，反之亦然。 如需詳細資訊，請參閱[for SQL Server 的 R 封裝管理](install-additional-r-packages-on-sql-server.md)。

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>從 SQL Server 的多個升級的問題

如果 SQL Server 2016 R Services 的執行個體先前已升級 9.0.1，當您執行 Microsoft R Server 9.1.0 的新安裝程式時，它會顯示一份所有有效的執行個體，並接著依預設會選取先前繫結的執行個體。 如果您繼續時，先前繫結的執行個體將會解除繫結。 如此一來，較早 9.0.1 會移除安裝，包括任何相關的封裝，但不是安裝 Microsoft R Server (9.1.0) 的新版本。

因應措施，您可以修改現有的 R 伺服器安裝，如下所示：
1. 在控制台中開啟**新增或移除程式**。
2. 找出 Microsoft R Server，然後按一下**變更/修改**。
3. 安裝程式啟動時，選取您想要繫結至 9.1.0 的執行個體。

Microsoft 的機器學習 Server 9.2.1 和 9.3 並沒有此問題。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>繫結或解除繫結會保留多個暫存資料夾

有時繫結和解除繫結作業無法清除暫存資料夾。
如果您發現具有類似名稱的資料夾，您可以將它移除安裝完成之後： R_SERVICES_<guid>

> [!NOTE]
> 請務必等候安裝完成。 可能需要很長的時間，若要移除與版本相關聯的 R 程式庫，然後再加入新的 R 程式庫。 當作業完成時，會移除暫存資料夾。

## <a name="see-also"></a>另請參閱

+ [安裝機器學習 Server for Windows （網際網路連線）](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [安裝機器學習 Server for Windows （離線）](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [機器學習伺服器中的已知的問題](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [從舊版的 R 伺服器的功能通知](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [已過時、 已停止或已變更的功能](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
