---
title: 升級資料層應用程式 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.upgradedacwizard.summary.f1
- sql13.swb.upgradedacwizard.reviewplan.f1
- sql13.swb.upgradedacwizard.upgradedac.f1
- sql13.swb.upgradedacwizard.selectpackage.f1
- sql13.swb.upgradedacwizard.reviewpolicy.f1
- sql13.swb.upgradedacwizard.selectoptions.f1
- sql13.swb.upgradedacwizard.checkdrift.f1
- sql13.swb.upgradedacwizard.introduction.f1
helpviewer_keywords:
- upgrade DAC
- data-tier application [SQL Server], upgrade
- wizard [DAC], upgrade
- How to [DAC], upgrade
ms.assetid: c117df94-f02b-403f-9383-ec5b3ac3763c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31b1fb369ee6b5007e79c96ebb7a536d6e2a147e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514042"
---
# <a name="upgrade-a-data-tier-application"></a>升級資料層應用程式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以使用升級資料層應用程式精靈或 Windows PowerShell 指令碼，將目前部署之資料層應用程式 (DAC) 的結構描述和屬性變更為符合新版 DAC 中所定義的結構描述和屬性。  
  
-   **開始之前：**  [選擇 DAC 升級選項](#ChoseDACUpgOptions)、 [限制事項](#LimitationsRestrictions)、 [必要條件](#Prerequisites)、 [安全性](#Security)、 [權限](#Permissions)  
  
-   **使用下列項目，升級 DAC**  [升級資料層應用程式精靈](#UsingDACUpgradeWizard)、 [PowerShell](#UpgradeDACPowerShell)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 DAC 升級是一種就地升級程序，可改變現有資料庫的結構描述，以符合新版 DAC 中所定義的結構描述。 在 DAC 封裝檔案中，會套用新版 DAC。 如需建立 DAC 封裝的詳細資訊，請參閱 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)。  
  
###  <a name="ChoseDACUpgOptions"></a> 選擇 DAC 升級選項  
 就地升級有四個升級選項：  
  
-   **忽略資料遺失** - 如果為 **True**，即使某些作業導致資料遺失，升級還是會繼續。 如果為 **False**，這些作業將會結束升級。 例如，如果目前資料庫中的資料表不在新 DAC 的結構描述中，則會在指定 **True** 時卸除資料表。 預設值為 **True**。  
  
-   **變更時封鎖** - 如果為 **True**，當資料庫結構描述不同於舊版 DAC 中所定義的資料庫結構描述時，就會結束升級。 如果為 **False**，即使偵測到變更，升級仍會繼續。 預設值為 **False**。  
  
-   **失敗時回復** - 如果為 **True**，升級將會包含在交易中，而如果發生錯誤，則會嘗試回復。 如果為 **False**，將會認可所有變更，而如果發生錯誤，您可能必須還原資料庫的先前備份。 預設值為 **False**。  
  
-   **略過原則驗證** - 如果為 **True**，則不會評估 DAC 伺服器選取原則。 如果為 **False**，則會評估原則，而如果發生驗證錯誤，則會結束升級。 預設值為 **False**。  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
 DAC 升級只能在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]或 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 或更新版本中執行。  
  
###  <a name="Prerequisites"></a> 必要條件  
 您必須在開始升級之前，進行完整資料庫備份。 如果升級時發生錯誤而無法回復其所有變更，您可能需要還原備份。  
  
 開始升級之前，有幾個您在驗證 DAC 封裝以及升級動作時應該採取的動作。 如需有關如何執行這些檢查的詳細資訊，請參閱＜ [Validate a DAC Package](../../relational-databases/data-tier-applications/validate-a-dac-package.md)＞。  
  
-   建議您不要使用來源不明或來源不受信任的 DAC 封裝來升級。 這類封裝可能包含惡意程式碼，因此可能會執行非預期的 Transact-SQL 程式碼，或是修改結構描述而造成錯誤。 在您使用來源不明或來源不受信任的封裝之前，請解除封裝 DAC 並檢查程式碼，例如預存程序或其他使用者定義程式碼。  
  
-   若您在部署最新版 DAC 之後變更目前的資料庫，某些變更可能會使升級無法成功完成，或因為升級而遭到移除。 您應該先產生並檢閱包含對資料庫所做之任何這類變更的報表。  
  
-   您必須產生要執行升級之結構描述變更的清單，並檢閱清單中是否有任何問題。  
  
 DAC 封裝中的應用程式名稱必須符合目前部署之 DAC 的應用程式名稱。 例如，如果目前的 DAC 具有應用程式名稱 **GeneralLedger**，您只能使用同樣具有應用程式名稱 **GeneralLedger**的 DAC 封裝來升級。  
  
 確定交易記錄空間足以記錄所有修改。  
  
###  <a name="Security"></a> 安全性  
 為了提高安全性，SQL Server 驗證登入會儲存在 DAC 封裝中，而且沒有密碼。 當您部署或升級此封裝時，此登入會建立為停用的登入，而且會產生密碼。 若要啟用登入，請使用具有 ALTER ANY LOGIN 權限的登入進行登入，並使用 ALTER LOGIN 來啟用登入，然後指派可以傳達給使用者的新密碼。 Windows 驗證登入不需要這項處理，因為這類登入的密碼不是由 SQL Server 所管理。  
  
####  <a name="Permissions"></a> Permissions  
 DAC 只能由 **sysadmin** 或 **serveradmin** 固定伺服器角色的成員，或是具有 **dbcreator** 固定伺服器角色及擁有 ALTER ANY LOGIN 權限的登入進行升級。 登入必須是現有資料庫的擁有者。 內建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員帳戶 (名稱為 **sa** ) 也可以升級 DAC。  
  
##  <a name="UsingDACUpgradeWizard"></a> 使用升級資料層應用程式精靈  
 **使用精靈升級 DAC**  
  
1.  在 **[物件總管]** 中，展開含有要升級 DAC 之執行個體的節點。  
  
2.  展開 [管理] 節點，然後展開 [資料層應用程式] 節點。  
  
3.  以滑鼠右鍵按一下要升級之 DAC 的節點，然後選取 [升級資料層應用程式...]  
  
4.  完成精靈對話方塊：  
  
    1.  [簡介頁面](#Introduction)  
  
    2.  [選取封裝頁面](#Select_dac_package)  
  
    3.  [檢閱原則頁面](#Review_policy)  
  
    4.  [偵測變更頁面](#Detect_change)  
  
    5.  [檢閱升級計畫](#ReviewUpgPlan)  
  
    6.  [摘要頁面](#Summary)  
  
    7.  [升級 DAC 頁面](#Upgrade)  
  
##  <a name="Introduction"></a> 簡介頁面  
 此頁面描述升級資料層應用程式的步驟。  
  
 **不要再顯示此頁面。** - 按一下此核取方塊，之後就不會再顯示此頁面。  
  
 **下一步 >** - 繼續進行 [選取封裝] 頁面。  
  
 **取消** - 結束精靈，而不升級 DAC。  
  
##  <a name="Select_dac_package"></a> 選取封裝頁面  
 使用此頁面來指定包含新版資料層應用程式的 DAC 封裝。 此頁面會在兩種狀態之間轉換。  
  
### <a name="select-the-dac-package"></a>選取 DAC 封裝  
 使用此頁面的初始狀態來選擇要部署的 DAC 封裝。 DAC 封裝必須是有效的 DAC 封裝檔案，而且必須有 .dacpac 副檔名。 DAC 封裝中的 DAC 應用程式名稱必須與目前 DAC 的應用程式名稱相同。  
  
 **DAC 封裝** - 指定包含新版資料層應用程式之 DAC 封裝的路徑和檔案名稱。 您可以選取方塊右邊的 **[瀏覽]** 按鈕，瀏覽到 DAC 封裝的位置。  
  
 **應用程式名稱** - 當撰寫 DAC 或是從資料庫擷取 DAC 時，顯示指派之 DAC 應用程式名稱的唯讀方塊。  
  
 **版本** - 當撰寫 DAC 或是從資料庫擷取 DAC 時，顯示指派之版本的唯讀方塊。  
  
 **描述** - 當撰寫 DAC 或是從資料庫擷取 DAC 時，顯示撰寫之描述的唯讀方塊。  
  
 **< 上一步** - 回到 [簡介] 頁面。  
  
 **下一步 >** - 將進度列顯示為確認選定檔案為有效 DAC 封裝的精靈。  
  
 **取消** - 結束精靈，而不升級 DAC。  
  
### <a name="validating-the-dac-package"></a>驗證 DAC 封裝  
 將進度列顯示為確認選定檔案為有效 DAC 封裝的精靈。 如果 DAC 封裝已經驗證，此精靈會繼續前往 **[檢閱原則]** 頁面。 如果檔案不是有效的 DAC 封裝，則精靈會停留在 **[選取 DAC 封裝]** 頁面上。 請選取另一個有效的 DAC 封裝，或是取消精靈並產生新的 DAC 封裝。  
  
 **正在驗證 DAC 的內容** - 報告驗證程序之目前狀態的進度列。  
  
 **< 上一步** - 回到 [選取封裝] 頁面的初始狀態。  
  
 **下一步 >** - 繼續進行最終版本的 [選取封裝] 頁面。  
  
 **取消** - 結束精靈，不部署 DAC。  
  
##  <a name="Review_policy"></a> 檢閱原則頁面  
 使用此頁面來檢閱評估 DAC 伺服器選取原則的結果 (如果 DAC 有原則的話)。 DAC 伺服器選取原則為選擇性，而且當它在 Microsoft Visual Studio 中撰寫時會指派給 DAC。 此原則會使用伺服器選取原則 Facet 來指定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體主控 DAC 所應該符合的條件。  
  
 **原則條件的評估結果** - 唯讀報表，顯示 DAC 伺服器選取原則中的條件評估是否成功。 評估每個條件的結果會在個別行上報告。  
  
 **忽略違反原則** - 使用這個核取方塊可在一個或多個原則條件失敗時繼續升級。 只有當您確定所有失敗的條件都不會阻礙 DAC 作業的成功時，才選取此選項。  
  
 **< 上一步** - 回到 [選取封裝] 頁面。  
  
 **下一步 >** - 繼續進行 [偵測變更] 頁面。  
  
 **取消** - 結束精靈，而不升級 DAC。  
  
##  <a name="Detect_change"></a> 偵測變更頁面  
 您可以使用此頁面報告此精靈檢查資料庫變更的結果，此結果會讓它的結構描述與 **msdb**中 DAC 中繼資料內儲存的結構描述定義不同。 例如，如果一開始部署 DAC 之後，已經使用 CREATE、ALTER 或 DROP 陳述式來從資料庫中加入、變更或移除物件。 此頁面會先顯示進度列，然後報告分析的結果。  
  
 **正在偵測變更。這可能需要幾分鐘時間** - 當精靈檢查目前的資料庫結構描述與 DAC 定義中的物件之間是否有差異時，將會顯示一個進度列。  
  
 **變更偵測結果:** - 表示分析已完成，並在底下報告結果。  
  
 **資料庫 DatabaseName 尚未變更** - 此精靈在資料庫內定義的物件與其在 DAC 定義內的對應物件之間並未偵測到任何差異。  
  
 **資料庫 DatabaseName 已變更** - 此精靈在資料庫內的物件與其在 DAC 定義內的對應物件之間偵測到變更。  
  
 **儘管變更可能遺失，還是繼續進行** - 指定您了解目前資料庫中的某些物件或資料將不會出現在新的資料庫中，但是您仍然願意繼續升級。 只有當您已經分析變更報表，並了解手動傳送新資料庫中所需之任何物件或資料所必須執行的步驟時，才應該選取這個按鈕。 如果您不確定，請按一下 **[儲存報表]** 按鈕儲存變更報表，然後按一下 **[取消]**。 分析報表、規劃如何在升級完成之後傳送任何必要的物件和資料，然後重新啟動精靈。  
  
 **儲存報表** - 按一下此按鈕，可儲存精靈在資料庫內的物件與其在 DAC 定義內的對應物件之間偵測到之變更的報表。 然後您可以檢閱報表，以決定升級完成之後是否需要採取動作，將報表中列出的某些物件或所有物件併入新的資料庫內。  
  
 **< 上一步** - 回到 [選取 DAC 封裝] 頁面。  
  
 **下一步 >** - 繼續進行 [選項] 頁面。  
  
 **取消** - 結束精靈，不部署 DAC。  
  
## <a name="options-page"></a>選項頁面  
 您可以使用此頁面針對升級選取失敗時回復選項。  
  
 **失敗時回復** - 選取此選項，可將升級併入精靈在發生錯誤時嘗試回復的交易。 如需有關此選項的詳細資訊，請參閱＜ [選擇 DAC 升級選項](#ChoseDACUpgOptions)＞。  
  
 **還原預設值** - 將此選項還原為其預設值 false。  
  
 **< 上一步** - 回到 [偵測變更] 頁面。  
  
 **下一步 >** - 繼續進行 [檢閱升級計畫] 頁面。  
  
 **取消** - 結束精靈，不部署 DAC。  
  
##  <a name="ReviewUpgPlan"></a> 檢閱升級計畫頁面  
 您可以使用此頁面檢閱升級程序所採取的動作。 只有當您確定升級不會產生問題時，才應該繼續進行。  
  
 **將使用以下動作升級 DAC。** - 檢閱顯示的資訊，以確保採取的動作將會是正確的。 [動作] 欄會顯示針對升級所執行的動作，例如 Transact-SQL 陳述式。 如果相關聯的動作可能會刪除資料， **[資料遺失]** 欄就會包含警告。  
  
 **重新整理** - 重新整理動作清單。  
  
 **儲存動作報表** - 將動作視窗的內容儲存至 HTML 檔案。  
  
 **儘管變更可能遺失，還是繼續進行** - 指定您了解目前資料庫中的某些物件或資料將不會出現在新的資料庫中，但是您仍然願意繼續升級。 只有當您已經分析變更報表，並了解手動傳送新資料庫中所需之任何物件或資料所必須執行的步驟時，才應該選取這個按鈕。 如果您不確定，請按一下 [儲存動作報告] 按鈕儲存變更報表並按一下 [儲存指令碼] 按鈕儲存 Transact-SQL 指令碼，然後按一下 [取消]。 分析報表和指令碼、規劃如何在升級完成之後傳送任何必要的物件和資料，然後重新啟動精靈。  
  
 **儲存指令碼** - 將用來執行升級的 Transact-SQL 陳述式儲存至文字檔。  
  
 **還原預設值** - 將此選項還原為其預設值 false。  
  
 **< 上一步** - 回到 [偵測變更] 頁面。  
  
 **下一步 >** - 繼續進行 [摘要] 頁面。  
  
 **取消** - 結束精靈，不部署 DAC。  
  
##  <a name="Summary"></a> 摘要頁面  
 您可以使用此頁面針對精靈在升級 DAC 時所採取動作進行最終檢閱。  
  
 **將使用以下設定升級您的 DAC** - 檢閱顯示的資訊，以確保採取的動作將會是正確的。 此視窗會顯示您選取要進行升級的 DAC，以及包含新版 DAC 的 DAC 封裝。 此視窗也會顯示目前的資料庫版本是否與目前的 DAC 定義相同，或資料庫是否已經變更。  
  
 **< 上一步** - 將您返回 [檢閱升級計畫] 頁面。  
  
 **下一步 >** - 部署 DAC，並在 [升級 DAC] 頁面中顯示結果。  
  
 **取消** - 結束精靈，不部署 DAC。  
  
##  <a name="Upgrade"></a> 升級 DAC 頁面  
 此頁面會報告升級作業成功或失敗。  
  
 **正在升級 DAC** - 報告為了升級 DAC 所採取的每個動作成功或失敗。 檢閱資訊以判斷每個動作成功或失敗。 發生錯誤的所有動作在 **[結果]** 資料行中都會有一個連結。 選取連結來檢視該動作的錯誤報告。  
  
 **儲存報表** - 選取此按鈕可將升級報表儲存到 HTML 檔案。 此檔案會報告每個動作的狀態，包括所有動作所產生的所有錯誤。 預設資料夾為 Windows 帳戶之文件資料夾中的 SQL Server Management Studio\DAC Packages 資料夾。  
  
 **完成** - 結束精靈。  
  
##  <a name="UpgradeDACPowerShell"></a> 使用 PowerShell  
 **在 PowerShell 指令碼中使用 IncrementalUpgrade() 方法升級 DAC**  
  
1.  建立 SMO Server 物件，並將它設為包含要升級之 DAC 的執行個體。  
  
2.  開啟 **ServerConnection** 物件，並連接到相同的執行個體。  
  
3.  使用 **System.IO.File** 以載入 DAC 封裝檔案。  
  
4.  使用 **add_DacActionStarted** 和 **add_DacActionFinished** 訂閱 DAC 升級事件。  
  
5.  設定 **DacUpgradeOptions**。  
  
6.  您可以使用 **IncrementalUpgrade** 方法來升級 DAC。  
  
7.  關閉用來讀取 DAC 封裝檔案的檔案資料流。  
  
### <a name="example-powershell"></a>範例 (PowerShell)  
 下列範例使用 MyApplication2017.dacpac 封裝中的新 DAC 版本來升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 預設執行個體上名為 MyApplication 的 DAC。  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication2017.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC upgrade events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Upgrade the DAC and close the package.  
$dacName  = "MyApplication"  
  
## Set the upgrade options.  
$upgradeProperties = New-Object Microsoft.SqlServer.Management.Dac.DacUpgradeOptions  
$upgradeProperties.blockonchanges = $true  
$upgradeProperties.ignoredataloss = $false  
$upgradeProperties.rollbackonfailure = $true  
$ upgradeProperties.skippolicyvalidation = $false  
  
## Upgrade the DAC  
$dacstore.IncrementalUpgrade($dacName, $dacType, $upgradeProperties)  
## Close the package file.  
$fileStream.Close()  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
