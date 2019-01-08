---
title: 升級 R 和 Python 元件-SQL Server Machine Learning 服務
description: R 和 Python 中 SQL Server 2016 Services 或 SQL Server 2017 Machine Learning 服務繫結至 Machine Learning Server 使用 sqlbindr.exe 升級。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 897f83e7272a47428d696802adf79ff816805486
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645447"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>升級 SQL Server 執行個體中的 機器學習 （R 和 Python） 元件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 中的 R 和 Python 整合包括開放原始碼和 Microsoft 的專屬套件。 在標準的 SQL Server 服務，根據 SQL Server 發行週期、 錯誤修正，以在最新版本，但沒有主要版本升級現有的封裝更新套件。 

不過，許多資料科學家已習慣新版的套件，可供使用。 SQL Server 2017 Machine Learning 服務 （資料庫） 和 SQL Server 2016 R Services （資料庫） 中，您可以取得[較新版本的 R 和 Python](#version-map)依*繫結*到**MicrosoftMachine Learning Server**。 

## <a name="what-is-binding"></a>何謂繫結？

繫結是交換出您的 R_SERVICES 與 PYTHON_SERVICES 資料夾，使用較新的可執行檔、 程式庫的內容，並從工具的安裝程序[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)。

與更新元件是在服務模型的參數。 而不是[SQL Server 產品生命週期](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017)，以[SQL Server 累計更新](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions)，現在符合您的服務更新[Microsoft R Server 和機器的支援時間表Learning Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)上[新式生命週期](https://support.microsoft.com/help/30881/modern-lifecycle-policy)。

元件版本和服務更新，除了繫結不會變更您的安裝的基本概念：R 和 Python 整合仍然是一部分的資料庫引擎執行個體中，授權會維持不變的 （不需要額外費用與繫結相關聯），和 SQL Server 支援原則仍會保留資料庫引擎。 本文的其餘部分說明繫結機制，以及每個版本的 SQL Server 的運作方式。

> [!NOTE]
> 繫結套用至 （資料庫內） 執行個體只會繫結至 SQL Server 執行個體。 繫結 （獨立式） 安裝無關。

**SQL Server 2017 繫結的考量**

For SQL Server 2017 Machine Learning 服務，您會在 Microsoft Machine Learning Server 開始提供其他套件，或透過您的較新版本已經時，才考慮繫結。

**SQL Server 2016 繫結的考量**

SQL Server 2016 R Services 的客戶，繫結會提供更新的 R 封裝，新的封裝不屬於原始的安裝 ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package))，以及[預先訓練模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)，全部都可以進一步在每個新的主要和次要版本的重新整理[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)。 繫結不會提供您的 Python 支援，這是 SQL Server 2017 功能。 

<a name="version-map"></a>

## <a name="version-map"></a>版本的對應

下表是版本對應，顯示跨版本車輛的套件版本，以便當您繫結至 Microsoft Machine Learning 伺服器 （先前稱為 R Server 的額外啟動的 Python 支援之前，您可以確定可能的升級路徑在 MLS 9.2.1)。 

請注意繫結並不保證的最新版本的 R 或 Anaconda。 當您繫結至 Microsoft Machine Learning 伺服器 (MLS) 時，您會取得安裝程式可能不會在網站上可用的最新版本的 R 或 Python 版本。

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

元件 |初始版本 | [R Server 9.0.1 （英文)](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
透過 R 的 Microsoft R Open (MRO) | R 3.2.2     | R 3.3.2 為基礎   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 （英文) |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| 荷屬安地列斯 | 9.0.1 （英文) |  9.1 |  9.2.1 |  9.3 |
[預先定型的模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| 荷屬安地列斯 | 9.0.1 （英文) |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 荷屬安地列斯 | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 荷屬安地列斯 | 1.0 |  1.0 |  1.0 |  1.0 |


[**SQL Server 2017 Machine Learning 服務**](../install/sql-machine-learning-services-windows-install.md)

元件 |初始版本 | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
透過 R 的 Microsoft R Open (MRO) | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
透過 Python 3.5 的 anaconda 4.2  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[預先定型的模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>元件升級的運作方式 

當您將現有安裝的 R 和 Python 繫結至 Machine Learning Server 時，會升級 R 和 Python 程式庫和可執行檔。 繫結執行者[Microsoft Machine Learning Server 安裝程式](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)現有 SQL Server 資料庫引擎執行個體，2017年或 2016年上執行安裝程式時擁有 R 或 Python 整合。 安裝程式偵測到現有的功能，並提示您重新繫結至 Machine Learning Server。 

在 C:\Program Files\Microsoft SQL Server\MSSQL14 內容的繫結。其會以較新的可執行檔和程式庫的 C:\Program Files\Microsoft\ML Server\R_SERVER 和 \PYTHON_SERVER 覆寫 MSSQLSERVER\R_SERVICES \PYTHON_SERVICES。

在此同時，服務模型也從 SQL Server 更新機制，翻轉至更頻繁的主要和次要版本循環的 Microsoft Machine Learning Server。 切換的支援原則是一個不錯的選擇，資料科學小組需要新一代 R 和 Python 模組以便他們的解決方案。 

+ 沒有繫結，R 和 Python 套件已修補的 bug 修正程式，當您安裝 SQL Server service pack 或累積更新 (CU)。 
+ 使用繫結，較新的套件版本可以套用至您的執行個體，獨立的 CU 發行排程，底下[新式生命週期原則](https://support.microsoft.com/help/30881/modern-lifecycle-policy)和版本的 Microsoft Machine Learning Server。 新式生命週期支援原則提供較短、 一年的存留時間更頻繁的更新。 後置繫結，您會繼續使用 R 和 Python 的未來更新 MLS 安裝程式，可供 Microsoft 下載網站上。

繫結，適用於 R 和 Python 功能。 也就是 Microsoft R Open （Anaconda）、 R 和 Python 功能的開放原始碼套件和專屬套件 RevoScaleR、 revoscalepy，等等。 繫結不會變更資料庫引擎執行個體的支援模型，並不會變更的 SQL Server 版本。

繫結是可反轉的。 您可以還原至 SQL Server 服務所[解除繫結執行個體](#bkmk_Unbind)和 reparing 您 SQL Server database engine 執行個體。

加總，繫結的步驟如下所示：

+ 使用現有的設定安裝 SQL Server 2016 R Services （或 SQL Server 2017 Machine Learning 服務） 啟動。
+ 判斷哪個版本的 Microsoft Machine Learning 伺服器具有您想要使用的升級的元件。
+ 下載並執行該版本的安裝程式。 安裝程式偵測到現有的執行個體，加入繫結 選項，並傳回相容的執行個體的清單。
+ 選擇您想要繫結，然後在完成安裝程式來執行繫結的執行個體。

使用者體驗方面的技術，以及如何與其保持不變。 唯一的差別是較新版本的封裝和可能附帶其他無法透過 SQL Server （例如 SQL Server 2016 R Services 的客戶的 MicrosoftML) 原本使用的封裝存在。

## <a name="bkmk_BindWizard"></a>繫結至 MLS 使用安裝程式

Microsoft Machine Learning 安裝程式偵測到 SQL Server 版本的現有功能，並叫用呼叫來變更繫結 SqlBindR.exe 公用程式。 就內部而言，SqlBindR 會鏈結至安裝程式，並間接使用。 稍後，您可以呼叫 SqlBindR 直接從命令列來執行特定的選項。

1. 在 SSMS 中，執行`SELECT @@version`，確認伺服器符合最低的組建需求。 

   最小值是 SQL Server 2016 R services [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276)並[CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。

1. 檢查 R 基底和 RevoScaleR 套件，以確認現有的版本低於您打算將其取代為版本。 SQL Server 2016 R services，R 基底套件是 3.2.2，RevoScaleR 8.0.3。

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

1. 關閉 SSMS 和任何其他需要 SQL Server 的開啟連接的工具。 繫結會覆寫的程式檔案。 如果 SQL Server 已開啟的工作階段，繫結將會失敗並繫結錯誤代碼 6。

1. 下載到您想要升級的執行個體的電腦上的 Microsoft Machine Learning Server。 我們建議[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)。

1. 解壓縮資料夾，並啟動 ServerSetup.exe，位於 MLSWIN93。

   ![Microsoft Machine Learning Server 安裝精靈](media/mls-921-installer-start.PNG)

1. 在 **設定安裝**，確認要升級的元件，然後檢閱相容的執行個體的清單。 

   這個步驟非常重要。

   在左側，選擇您想要保留或升級每一項功能。 您無法升級某些功能，而不是其他項目。 空白的核取方塊中移除該功能，假設目前已安裝的功能。 螢幕擷取畫面、 執行個體的 SQL Server 2016 R Services (MSSQL13)，會選取 R 和 R 預先定型的模型版本。 此設定是有效的因為 SQL Server 2016 支援 R 但沒有 Python 支援。

   如果您要升級 SQL Server 2016 R Services 上的元件，請勿選取 [Python] 功能。 您無法將 Python 新增至 SQL Server 2016 R Services。

   在右側，選取 執行個體名稱旁的核取方塊。 如果沒有列出任何執行個體，您會有不相容的組合。 如果您未選取執行個體，建立新的 Machine Learning Server 獨立安裝時，與 SQL Server 程式庫不會變更。 如果您無法選取執行個體，它可能無法在[SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。 

    ![設定安裝步驟](media/mls-931-installer-mssql13.png)

1. 在 **授權合約**頁面上，選取**我接受這些條款**Machine Learning 伺服器接受授權條款。 

1. 在後續頁面中，提供額外的授權條款，選取，例如 Microsoft R Open 或 Python Anaconda 散發套件的任何開放原始碼元件的同意。

1. 在 **就快完成了**頁面上，記下的安裝資料夾。 預設資料夾是 \Program Files\Microsoft\ML 伺服器。

    如果您想要變更安裝資料夾，按一下**進階**返回精靈的第一頁。 不過，您必須重複所有先前的選取項目。

在安裝過程中，會取代任何 SQL Server 所使用的 R 或 Python 程式庫，並啟動控制板會更新以使用較新的元件。 如此一來，如果預設的 R_SERVICES 資料夾使用的執行個體先前的程式庫，在升級後會移除這些程式庫，Launchpad 服務的屬性都會變更為使用新的位置中的程式庫。

繫結會影響這些資料夾的內容：C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library 會取代 C:\Program Files\Microsoft\ML Server\R_SERVER 的內容。 Microsoft Machine Learning Server 安裝程式建立第二個資料夾和其內容。 

如果升級失敗，請檢查[SqlBindR 錯誤碼](#sqlbindr-error-codes)如需詳細資訊。

## <a name="confirm-binding"></a>確認繫結

重新檢查以確認您有較新版本的 R 和 RevoScaleR 的版本。 您可以使用隨附在您的資料庫引擎執行個體中的 R 套件的 R 主控台取得封裝資訊：

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

針對繫結至 Machine Learning Server 9.3 SQL Server 2016 R Services，R 基底套件能 3.4.3、 RevoScaleR 應為 9.3，而且您也應該 MicrosoftML 9.3。 

如果您新增預先定型的模型，模型會內嵌 MicrosoftML 文件庫中，而且您可以透過 MicrosoftML 函式呼叫它們。 如需詳細資訊，請參閱 < [MicrosoftML 的 R 範例](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)。

## <a name="offline-binding-no-internet-access"></a>離線的繫結 （沒有網際網路存取）

沒有網際網路連線的系統，可以將安裝程式和.cab 檔案下載到連接網際網路的電腦上，並再將檔案傳輸到隔離的伺服器。 

安裝程式 (ServerSetup.exe) 包含 RevoScaleR、 MicrosoftML、 olapR （sqlRUtils） 的 Microsoft 套件。 .Cab 檔案提供其他核心元件。 例如，"SRO 」 封包提供 R Open，Microsoft 發佈的開放原始碼。

下列指示說明如何放置進行離線安裝檔案。

1. MLS 安裝程式下載。 它會下載為一個單一的壓縮檔。 我們建議[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)，但您也可以安裝[舊版](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)。

1. 下載的.cab 檔。 下列連結是 9.3 的版本。 如果您需要更早版本時，可以中找到其他連結[R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)。 您應該記得，Python/Anaconda 只能加入至 SQL Server 2017 Machine Learning 服務執行個體。 預先定型的模型存在 R 和 Python;.cab 會提供您使用的語言中的模型。

    | 功能 | 下載 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 預先定型的模型 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. 將.zip 和.cab 檔案傳輸至目標伺服器。

1. 在伺服器上，輸入`%temp%`中 [執行] 命令，以取得實體暫存目錄的位置。 機器的實體路徑而有所不同，但它通常是`C:\Users\<your-user-name>\AppData\Local\Temp`。

1. 將.cab 檔案放在 %temp%資料夾中。

1. 解壓縮安裝程式。

1. 執行 ServerSetup.exe 並遵循螢幕上的提示完成安裝。

## <a name="bkmk_BindCmd"></a>命令列作業

在執行 Microsoft Machine Learning 伺服器之後，呼叫了 SqlBindR.exe 命令列公用程式會變成可用，您可以使用進一步繫結作業中。 例如，如果您決定要反轉的繫結，您可以重新執行安裝程式或使用命令列公用程式。 此外，您可以使用這項工具，例如檢查相容性和可用性。

> [!TIP]
> 找不到 SqlBindR？ 您可能還沒有執行安裝程式。 SqlBindR 執行 Machine Learning Server 安裝程式之後，只是可用的。

1. 以系統管理員身分開啟命令提示字元，並瀏覽至包含 sqlbindr.exe 的資料夾。 預設位置是 C:\Program Files\Microsoft\MLServer\Setup

2. 輸入下列命令以檢視可用的執行個體清單︰ `SqlBindR.exe /list`
  
   請記下列出的完整執行個體名稱。 例如，執行個體名稱可能是 MSSQL14。MSSQLSERVER 是預設執行個體，或伺服器名稱類似。MYNAMEDINSTANCE。

3. 執行**SqlBindR.exe**命令搭配*繫結/* 引數，並指定要升級之執行個體名稱使用上一個步驟中所傳回的執行個體名稱。

   例如，若要升級的預設執行個體，請輸入：  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 在完成升級之後，重新啟動 Launchpad 服務已經過修改的任何執行個體相關聯。

## <a name="bkmk_Unbind"></a>還原或解除繫結執行個體

您可以在初始安裝的 R 和 Python 的元件，建立 SQL Server 安裝程式來還原繫結的執行個體。 有三個部分，若要再還原至 SQL Server 服務。

+ [步驟 1:從 Microsoft Machine Learning Server 解除繫結](#step-1-unbind)
+ [步驟 2:將執行個體還原為原始狀態](#step-2-restore)
+ [步驟 3:重新安裝任何新增至安裝的套件](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>步驟 1：解除繫結

您有兩個步驟回復繫結的選項： 重新重新執行安裝程式，或使用 SqlBindR 命令列公用程式。

#### <a name="bkmk_wizunbind"></a> 解除繫結使用安裝程式

1. 找出 Machine Learning 伺服器安裝程式。 如果您已移除安裝程式，您可能需要再下載一次，或將它複製從另一部電腦。
2. 請務必在您想要解除繫結的執行個體的電腦上執行安裝程式。
2. 安裝程式會識別會被解除繫結的本機執行個體。
3. 取消選取您想要還原為原始設定的執行個體旁邊的核取方塊。
4. 接受授權合約。 您必須在安裝時，指出您接受授權條款，甚至是。
5. 按一下 **[完成]**。 此程序需要一些時間。

#### <a name="bkmk_cmdunbind"></a> 解除繫結使用命令列

1. 開啟命令提示字元並瀏覽至包含 **sqlbindr.exe** 的資料夾，如上一節所述。

2. 搭配 */unbind* 引數執行 **SqlBindR.exe** 命令，並指定執行個體。

   例如，下列命令會還原預設執行個體：
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>步驟 2：修復 SQL Server 執行個體

執行 SQL Server 安裝程式修復具有 R 和 Python 功能的資料庫引擎執行個體。 系統會保留現有的更新，但如果您錯過任何的 SQL Server 服務更新 R 和 Python 套件，此步驟適用於這些修補程式。

或者，這是更多工作，但您可能也完全解除安裝並重新安裝資料庫引擎執行個體，然後套用所有的服務更新。

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>步驟 3：新增任何第三方套件

您可能已經將其他開放原始碼或協力廠商封裝加入您的套件程式庫。 反轉繫結參數的預設套件程式庫的位置，因為您必須重新安裝至程式庫，現在使用 R 和 Python 套件。 如需詳細資訊，請參閱 <<c0> [ 預設封裝](installing-and-managing-r-packages.md)，[安裝新的 R 套件](install-additional-r-packages-on-sql-server.md)，並[安裝新的 Python 套件](../python/install-additional-python-packages-on-sql-server.md)。

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR.exe 命令語法

### <a name="usage"></a>使用量

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>參數

|名稱|描述|
|------|------|
|*list*| 顯示目前電腦上所有 SQL 資料庫執行個體識別碼的清單|
|*bind*| 將指定的 SQL 資料庫執行個體升級到最新版 R Server，並確保執行個體自動取得 R Server 的未來升級|
|*unbind*|從指定的 SQL 資料庫執行個體解除安裝最新版的 R Server，並防止未來的 R Server 升級影響執行個體|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>繫結錯誤

MLS Installer 和 SqlBindR 這兩個會傳回下列錯誤碼和訊息。

|錯誤碼  | 訊息           | 詳細資料               |
|------------|-------------------|-----------------------|
|繫結錯誤 0 | 好了 （成功） | 繫結傳遞，未發生錯誤。 |
|繫結錯誤 1 | 無效的引數 | 語法錯誤。 |
|繫結錯誤 2 | 無效的動作 | 語法錯誤。 |
|繫結錯誤 3 | 無效的執行個體 | 執行個體存在，但不是有效的繫結。 |
|繫結錯誤 4 | 不是可繫結 | |
|繫結錯誤 5 | 已繫結 | 您執行了 *bind* 命令，但指定的執行個體已經繫結。 |
|繫結錯誤 6 | 繫結失敗 | 解除繫結執行個體時發生錯誤。 如果您執行 MLS 安裝程式，但不選取任何功能，就會發生此錯誤。 繫結需要您同時選取 MSSQL 執行個體和 R 和 Python，假定執行個體是 SQL Server 2017。 如果 SqlBindR 無法寫入 Program Files 資料夾，也會發生此錯誤。 開啟的工作階段或 SQL Server 的控制代碼會發生這個錯誤。 如果您收到這個錯誤，重新啟動電腦，並啟動任何新的工作階段之前的重做的繫結的步驟。|
|繫結錯誤 7 | 未繫結 | Database engine 執行個體有 R Services 或 SQL Server Machine Learning 服務。 Microsoft Machine Learning 伺服器不一定會執行個體。 |
|繫結錯誤 8 | 解除繫結失敗 | 解除繫結執行個體時發生錯誤。 |
|繫結錯誤 9 | 找不到任何執行個體 | 在此電腦上找不到任何資料庫引擎執行個體。 |

## <a name="known-issues"></a>已知問題

此區段會列出使用 SqlBindR.exe 公用程式，或升級可能會影響 SQL Server 執行個體的 Machine Learning Server 的特定已知的問題。

### <a name="restoring-packages-that-were-previously-installed"></a>還原先前安裝的套件

如果您升級到 Microsoft R Server 9.0.1 （英文)，該版本 SqlBindR.exe 版本無法還原原始封裝或 R 元件完全，要求使用者執行個體上執行 SQL Server 修復套用所有的服務版本，然後再重新啟動執行個體。

新版 SqlBindR 自動還原原始的 R 功能，而不需要重新安裝 R 元件，或是重新修補伺服器。 不過，您必須安裝可能會在初始安裝後新增的任何 R 封裝更新。

如果您已安裝以及共用封裝中使用封裝管理角色，這項工作會更容易： 您可以使用 R 命令，在同步處理已安裝的套件，在資料庫中，使用記錄在檔案系統，反之亦然。 如需詳細資訊，請參閱 < [SQL Server 的 R 封裝管理](install-additional-r-packages-on-sql-server.md)。

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>從 SQL Server 的多個升級的問題

如果您先前已升級至 9.0.1 （英文），SQL Server 2016 R Services 的執行個體，當您執行適用於 Microsoft R Server 9.1.0 新的安裝程式時，它會顯示一份所有有效的執行個體，並接著選取 預設的 先前的繫結的執行個體。 如果您繼續時，先前的繫結的執行個體將會解除繫結。 如此一來，先前 9.0.1 （英文） 會移除安裝，包括任何相關的封裝，但未安裝 Microsoft R server (9.1.0) 新的版本。

因應措施，您可以修改現有的 R 伺服器安裝，如下所示：
1. 在控制台中，開啟**新增或移除程式**。
2. 找出 Microsoft R Server，然後按一下**變更/修改**。
3. 當安裝程式啟動時，選取您想要繫結至 9.1.0 的執行個體。

Microsoft Machine Learning Server 9.2.1 和 9.3 並沒有此問題。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>繫結或解除繫結會保留多個暫存資料夾

有時候繫結和解除繫結的作業無法清除暫存資料夾。
如果您發現這類名稱的資料夾，您可以移除它，在安裝完成之後：R_SERVICES_<guid>

> [!NOTE]
> 請務必等候安裝完成。 可能需要很長的時間，移除與版本相關聯的 R 程式庫，然後加入新的 R 程式庫。 當作業完成時，會移除暫存資料夾。

## <a name="see-also"></a>另請參閱

+ [安裝 Machine Learning Server for Windows （網際網路連線）](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [安裝 Machine Learning Server for Windows （離線）](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [在 Machine Learning Server 中的已知的問題](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [從舊版的 R Server 的功能宣告](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [已過時、 已停止或已變更的功能](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
