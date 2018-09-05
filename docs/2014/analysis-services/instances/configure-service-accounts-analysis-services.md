---
title: 設定服務帳戶 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services], logon accounts
- logon accounts [Analysis Services]
- accounts [Analysis Services]
- logon accounts [Analysis Services], about logon accounts
ms.assetid: b481bd51-e077-42f6-8598-ce08c1a38716
caps.latest.revision: 52
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12c58fcc3e844e820dbea02e93b52854dc25f05f
ms.sourcegitcommit: 2a47e66cd6a05789827266f1efa5fea7ab2a84e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348359"
---
# <a name="configure-service-accounts-analysis-services"></a>設定服務帳戶 (Analysis Services)
  [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)中記載如何佈建適用於整個產品範圍的帳戶，該主題提供適用於所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務 (包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]) 的全方位服務帳戶資訊。 如需了解有效的帳戶類型、由安裝程式指派的 Windows 權限、檔案系統權限、登錄權限等，請參閱該主題。  
  
 本主題提供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的補充資訊，包含表格式和叢集安裝所需的其他權限。 其中也涵蓋支援伺服器作業所需的權限。 例如，您可以在服務帳戶底下設定要排除的處理和查詢作業 - 在這個情況下，您將需要授與其他權限來讓這個動作生效。  
  
-   [指派給 Analysis Services 的 Windows 權限](#bkmk_winpriv)  
  
-   [指派給 Analysis Services 的檔案系統權限](#bkmk_FilePermissions)  
  
-   [授與特定伺服器作業的其他權限](#bkmk_tasks)  
  
 另一個設定步驟 (此處未記載) 是註冊 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體和服務帳戶的服務主要名稱 (SPN)。 這個步驟可在雙躍點狀況下啟用從用戶端應用程式到後端資料來源的傳遞驗證。 這個步驟僅適用於針對 Kerberos 限制委派設定的服務。 如需進一步指示，請參閱＜ [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md) ＞。  
  
## <a name="logon-account-recommendations"></a>登入帳戶建議  
 在容錯移轉叢集中，Analysis Services 的所有執行個體都應該都設定為使用 Windows 網域使用者帳戶。 將相同的帳戶指派給所有執行個體。 請參閱 [如何將 Analysis Services 叢集化](http://msdn.microsoft.com/library/dn736073.aspx) 如需詳細資訊。  
  
 獨立執行個體應該使用預設虛擬帳戶**NT Service\MSSQLServerOLAPService**的預設執行個體，或 **NT Service\MSOLAP$ * * * 執行個體名稱*的具名執行個體。 這項建議適用於所有伺服器模式中的 Analysis Services 執行個體，作業系統為 Windows Server 2008 R2 和更新版本，而 Analysis Services 為 SQL Server 2012 和更新版本。  
  
## <a name="granting-permissions-to-analysis-services"></a>授與權限給 Analysis Services  
 本節說明 Analysis Services 對於本機的內部作業 (例如啟動可執行檔、讀取組態檔，以及從資料目錄載入資料庫) 所需的權限。 如果您是要尋找為外部資料存取設定權限，以及與其他服務和應用程式的互通性的指引，請參閱本主題中的 [授與特定伺服器作業的其他權限](#bkmk_tasks) 。  
  
 針對內部作業，Analysis Services 中的權限持有者不是登入帳戶，而是包含個別服務 SID 的安裝程式建立的本機 Windows 安全性群組。 指派權限給安全性群組的動作與舊版的 Analysis Services 一致。 同時，登入帳戶可能隨著時間變更，但個別服務 SID 與本機安全性群組在伺服器安裝的存留期都維持不變。 針對 Analysis Services，這會使得安全性群組，而不是登入帳戶，成為持有權限的較佳選擇。 每當您手動授與權限給服務執行個體，不論是檔案系統權限或 Windows 權限，請務必將為伺服器執行個體建立的權限授與本機安全性群組。  
  
 遵循模式之安全性群組的名稱。 前置詞一律是`SQLServerMSASUser$`，後面接著電腦名稱，結尾是執行個體名稱。 預設執行個體是`MSSQLSERVER`。 具名執行個體是在設定期間指定的名稱。  
  
 您可以在本機安全性設定中看到這個安全性群組：  
  
-   執行 compmgmt.msc |**本機使用者和群組** | **群組** | `SQLServerMSASUser$`\<伺服器名稱 >`$MSSQLSERVER` （適用於預設執行個體）。  
  
-   按兩下安全性群組以檢視其成員。  
  
 群組的唯一成員是個別服務 SID。 旁邊就是登入帳戶。 登入帳戶名稱是表面，在此提供內容給個別服務 SID。 如果您後續變更登入帳戶，然後返回此頁面，會發現安全性群組和個別服務 SID 不會變更，但是登入帳戶標籤則不同。  
  
##  <a name="bkmk_winpriv"></a> 指派給 Analysis Services 服務帳戶的 Windows 權限  
 Analysis Services 需要來自作業系統的權限，才能進行服務啟動，以及要求系統資源。 需求會依照伺服器模式以及執行個體是否已叢集而改變。 如果您不熟悉 Windows 權限，請參閱 [權限](http://msdn.microsoft.com/library/windows/desktop/aa379306\(v=vs.85\).aspx) 和 [權限常數 (Windows)](/windows/desktop/SecAuthZ/privilege-constants) 以了解詳細資訊。  
  
 Analysis Services 的所有執行個體都需有 **[以服務方式登入]** (SeServiceLogonRight) 權限。 SQL Server 安裝程式會為您指派安裝期間所指定之服務帳戶的權限。 對於以多維度和資料採礦模式執行的伺服器而言，這對獨立伺服器安裝而言是 Analysis Services 服務帳戶所需的唯一 Windows 權限，而且它是安裝程式為 Analysis Services 所設定的唯一權限。 至於叢集和表格式執行個體，則是必須手動新增其他 Windows 權限。  
  
 容錯移轉叢集執行個體 (在表格式或多維度模式中) 必須具備 **[提升排程優先權]** (SeIncreaseBasePriorityPrivilege)。  
  
 表格式執行個體會使用下列三種其他權限，您必須在安裝執行個體之後手動授與。  
  
|||  
|-|-|  
|**增加處理程序工作組** (SeIncreaseWorkingSetPrivilege)|透過 **[使用者]** 安全性群組，此權限預設可供所有使用者使用。 如果您藉由移除這個群組的權限來鎖定伺服器，Analysis Services 可能會無法啟動，並會記錄以下錯誤：「用戶端沒有這項特殊權限。」 發生這個錯誤時，請將權限授與適當的 Analysis Services 安全性群組，藉以將權限還原到 Analysis Services。|  
|**調整處理序的記憶體配額** (SeIncreaseQuotaSizePrivilege)|如果處理程序擁有的資源不足以完成它的執行 (受限於針對執行個體所建立的記憶體臨界值)，則可使用這個權限來要求更多記憶體。|  
|**鎖定記憶體中的分頁** (SeLockMemoryPrivilege)|只有在完全關閉分頁時才需要這個權限。 根據預設，表格式伺服器執行個體使用 Windows 分頁檔，但您可以防止它藉由設定使用 Windows 分頁`VertiPaqPagingPolicy`設為 0。<br /><br /> `VertiPaqPagingPolicy` 設為 1 （預設值），指示表格式伺服器執行個體使用 Windows 分頁檔。 配置並未鎖定，可視需要允許 Windows 移出分頁。 由於已使用分頁，所以不需鎖定記憶體中的分頁。 因此，針對預設設定 (其中`VertiPaqPagingPolicy`= 1)，您不需要授與**在記憶體中鎖定分頁**表格式執行個體的權限。<br /><br /> `VertiPaqPagingPolicy` 設為 0。 如果您針對 Analysis Services 關閉分頁，即會假設已將 **[鎖定記憶體中的分頁]** 權限授與表格式執行個體，而鎖定配置。 指定這個設定和 **[鎖定記憶體中的分頁]** 權限，Windows 便無法在系統處於記憶體不足壓力的情況下，移出針對 Analysis Services 所做之記憶體配置的分頁。 Analysis Services 會仰賴**在記憶體中鎖定分頁**權限，才能在`VertiPaqPagingPolicy`= 0。 請注意，不建議關閉 Windows 分頁。 這將會提高作業產生記憶體不足之錯誤的機率，而這些作業在允許分頁的情況下可能就會成功。 請參閱[Memory Properties](../server-properties/memory-properties.md)如需詳細資訊`VertiPaqPagingPolicy`。|  
  
#### <a name="to-view-or-add-windows-privileges-on-the-service-account"></a>檢視或新增服務帳戶的 Windows 權限  
  
1.  執行 GPEDIT.msc | 本機電腦原則 | 電腦組態 | Windows 設定 | 安全性設定 | 本機原則 | 使用者權限指派。  
  
2.  檢閱現有的原則包含`SQLServerMSASUser$`。 這是可以在已安裝 Analysis Services 的電腦上找到的本機安全性群組。 Windows 權限和檔案資料夾權限都會授與這個安全性群組。 按兩下 **[以服務方式登入]** 原則，以查看在系統上指定安全性群組的方式。 安全性群組的完整名稱會根據您是否安裝 Analysis Services 來做為具名執行個體而改變。 新增帳戶權限時，請使用這個安全性群組，而不要使用實際的服務帳戶。  
  
3.  若要在 GPEDIT 中新增帳戶權限，請以滑鼠右鍵按一下 **[增加處理程序工作組]** ，然後選取 **[屬性]**。  
  
4.  按一下 **[加入使用者或群組]**。  
  
5.  輸入 Analysis Services 執行個體的使用者群組。 請記住，服務帳戶是本機安全性群組的成員，要求您預先附加本機電腦名稱做為帳戶的網域。  
  
     下列清單顯示的兩個範例分別為名為 "SQL01-WIN12" 之電腦上的預設執行個體及名為 "Tabular" 的具名執行個體，其中電腦名稱為本機網域。  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$MSSQLSERVER  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$TABULAR  
  
6.  針對 **[調整處理序的記憶體配額]** 重複執行，以及選擇性地針對 **[鎖定記憶體中的分頁]** 或 **[提升排程優先權]** 重複執行。  
  
> [!NOTE]  
>  舊版安裝程式不小心將 Analysis Services 服務帳戶加入 **Performance Log Users** 群組。 雖然已修正此缺點，但是現有的安裝可能會具有此不必要的群組成員資格。 由於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務帳戶不需要 **[Performance Log Users]** 群組中的成員資格，因此您可以從群組中移除。  
  
##  <a name="bkmk_FilePermissions"></a> 指派給 Analysis Services 服務帳戶的檔案系統權限  
  
> [!NOTE]  
>  如需與每個程式資料夾相關聯的權限清單，請參閱 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) 。  
>   
>  如需與 IIS 組態和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 相關的檔案權限資訊，請參閱[設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
 伺服器作業所需的所有檔案系統權限 (包括從指定的資料夾載入及卸載資料庫所需的權限) 會在安裝期間由 SQL Server 安裝程式指派。  
  
 資料檔、程式執行檔、設定檔、記錄檔及暫存檔的權限持有者是由 SQL Server 安裝程式所建立的本機安全性群組。  
  
 有一個針對您安裝之每個執行個體所建立的安全性群組。 可能是具名執行個體命名的安全性群組**SQLServerMSASUser$ MSSQLSERVER**的預設執行個體，或`SQLServerMSASUser$`\<伺服器名稱 >$\<執行個體名稱 > 的具名執行個體。 安裝程式會為此安全性群組佈建執行伺服器作業所需的檔案權限。 如果您在 \MSAS12.MSSQLSERVER\OLAP\BIN 目錄上檢查安全性權限，就會看見安全性群組 (而不是服務帳戶或其個別服務 SID) 是該目錄的權限持有者。  
  
 安全性群組只包含一個成員： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體啟動帳戶的個別服務安全性識別碼 (SID)。 安裝程式會將個別服務 SID 新增到本機安全性群組。 相較於資料庫引擎，SQL Server 安裝程式佈建 Analysis Services 的方式有一個很小但明顯的差異，那就是搭配 SID 成員資格使用本機安全性群組。  
  
 如果您認為檔案權限已毀損，請依照下列步驟來確認是否仍已正確佈建服務：  
  
1.  使用服務控制命令列工具 (sc.exe) 來取得預設服務執行個體的 SID。  
  
     `SC showsid MSSqlServerOlapService`  
  
     針對具名執行個體 (其中執行個體名稱為 Tabular)，請使用下列語法：  
  
     `SC showsid MSOlap$Tabular`  
  
2.  使用**Computer Manager** | **本機使用者和群組** | **群組**檢查 SQLServerMSASUser$的成員資格\<伺服器名稱 >$\<執行個體名稱 > 安全性群組。  
  
     成員 SID 應該與來自步驟 1 的個別服務 SID 相符。  
  
3.  使用 [電腦管理員]  |  |  | [MSASxx.MSSQLServer] | []  |  ，確認已將資料夾安全性屬性授與步驟 2 中的安全性群組。  
  
> [!NOTE]  
>  請勿移除或修改 SID。 若要還原不小心刪除的個別服務 SID，請參閱[ http://support.microsoft.com/kb/2620201 ](http://support.microsoft.com/kb/2620201)。  
  
 **更多關於個別服務 SID 的資訊**  
  
 每個 Windows 帳戶都有相關聯的 [SID](http://en.wikipedia.org/wiki/Security_Identifier)，但服務也可能有 SID，因此稱為個別服務 SID。 個別服務 SID 是在安裝服務執行個體時所建立，做為服務的唯一、永久固定項目。 個別服務 SID 是自服務名稱產生的本機電腦層級 SID。 在預設執行個體上，其使用者易記名稱是 NT SERVICE\MSSQLServerOLAPService。  
  
 個別服務 SID 的優點是它允許可任意變更更普遍可見的登入帳戶，而不會影響檔案權限。 例如，假設您已安裝兩個 Analysis Services 執行個體 (預設執行個體和具名執行個體)，這兩個執行個體都在相同的 Windows 使用者帳戶下執行。 共用登入帳戶時，每個服務執行個體就會具有唯一的個別服務 SID。 這個 SID 與登入帳戶的 SID 不同。 個別服務 SID 是用於檔案權限和 Windows 權限。 相反地，登入帳戶 SID 用於驗證和授權案例，不同的 SID 用於不同用途。  
  
 由於 SID 是不可變的，因此，不論您變更服務帳戶的頻率為何，都能永遠使用服務安裝期間建立的檔案系統 ACL。 身為新增的安全性措施，ACL 透過 SID 指定權限，即使其他服務在相同帳戶下執行，也能確保只有一個服務執行個體存取程式可執行檔和資料夾，因此可提高安全性。  
  
##  <a name="bkmk_tasks"></a> 為特定伺服器作業授與其他 Analysis Services 權限  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在用來啟動 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之服務帳戶 (或登入帳戶) 的安全性內容中執行一些工作，並在要求工作之使用者的安全性內容中執行其他工作。  
  
 下表描述支援以服務帳戶執行工作所需的其他權限。  
  
|伺服器作業|工作項目|理由|  
|----------------------|---------------|-------------------|  
|遠端存取外部關聯式資料來源|建立服務帳戶的資料庫登入|處理是指從外部資料來源 (通常是關聯式資料庫) 擷取資料，再接著載入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。 擷取外部資料的其中一個認證選項是使用服務帳戶。 只有在建立服務帳戶的資料庫登入，並授與來源資料庫的讀取權限時，此認證選項才有效。 如需如何針對此工作使用服務帳戶選項的詳細資訊，請參閱[設定模擬選項 &#40;SSAS - 多維度&#41;](../multidimensional-models/set-impersonation-options-ssas-multidimensional.md)。 同樣地，如果以 ROLAP 做為儲存模式，也可以使用相同的模擬選項。 在此情況下，帳戶也必須對來源資料具有寫入權限才能處理 ROLAP 分割區 (亦即，儲存彙總)。|  
|DirectQuery|建立服務帳戶的資料庫登入|DirectQuery 是用來查詢外部資料集的表格式功能，這些資料集可能太大，而無法容納在表格式模型內，或者具有其他特性，使得 DirectQuery 比預設的記憶體中儲存選項更適合。 DirectQuery 模式中可用的其中一個連接選項是使用服務帳戶。 同樣地，只有在服務帳戶具有資料庫登入和目標資料來源的讀取權限時，此選項才有效。 如需如何針對此工作使用服務帳戶選項的詳細資訊，請參閱[設定模擬選項 &#40;SSAS - 多維度&#41;](../multidimensional-models/set-impersonation-options-ssas-multidimensional.md)。 或者，您可以使用目前使用者的認證來擷取資料。 在大多數情況下，此選項需要雙躍點連線，因此請務必設定服務帳戶進行 Kerberos 限制委派，以便服務帳戶可以將識別委派給下游伺服器。 如需詳細資訊，請參閱 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md)。|  
|遠端存取其他 SSAS 執行個體|將服務帳戶新增到在遠端伺服器上定義的 Analysis Services 資料庫角色|遠端分割區及其他遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的參考連結物件，都是需要遠端電腦或裝置權限的系統功能。 當使用者建立及擴展遠端分割區，或者設定連結物件時，該作業會在目前使用者的安全性內容中執行。 如果您之後自動化這些作業， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在其服務帳戶的安全性內容中存取遠端執行個體。 若要在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的遠端執行個體上存取連結物件，登入帳戶必須具有在遠端執行個體上讀取適當物件的權限，例如對特定維度的「讀取」權限。 同樣地，使用遠端分割區需要在遠端執行個體上具有管理權限的服務帳戶。 您可以透過將允許的作業關聯到特定物件的角色，來授與遠端 Analysis Services 執行個體的這類權限。 請參閱[授與資料庫權限 &#40;Analysis Services&#41;](../multidimensional-models/grant-database-permissions-analysis-services.md)，以取得如何授與完整控制權限以允許處理和查詢作業的相關指示。 如需遠端資料分割的詳細資訊，請參閱[建立及管理遠端資料分割 &#40;Analysis Services&#41;](../multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)。|  
|回寫|將服務帳戶新增到在遠端伺服器上定義的 Analysis Services 資料庫角色|在用戶端應用程式中啟用時，回寫是多維度模型功能，可在資料分析期間建立新的資料值。 如果已在維度或 Cube 內啟用回寫， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務帳戶就必須針對來源 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫中的回寫資料表具備寫入權限。 如果這個資料表不存在而需要建立，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務帳戶在指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中，也必須有建立資料表的權限。|  
|寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫中的查詢記錄資料表|建立服務帳戶的資料庫登入並指派查詢記錄表格的寫入權限|您可以啟用查詢記錄，以收集資料庫資料表中的使用量資料進行後續分析。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務帳戶對指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的查詢記錄資料表，必須具有寫入權限。 如果這個資料表不存在而需要建立，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 登入帳戶在指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中，也必須有建立資料表的權限。 如需詳細資訊，請參閱 [Improve SQL Server Analysis Services Performance with the Usage Based Optimization Wizard (部落格)](http://www.mssqltips.com/sqlservertip/2876/improve-sql-server-analysis-services-performance-with-the-usage-based-optimization-wizard/) 和 [Query Logging in Analysis Services (部落格)](http://weblogs.asp.net/miked/archive/2013/07/31/query-logging-in-analysis-services.aspx)。|  
  
## <a name="see-also"></a>另請參閱  
 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [SQL Server 服務帳戶和個別服務 SID （部落格）](http://www.travisgan.com/2013/06/sql-server-service-account-and-per.html)   
 [SQL Server 使用服務 SID 提供服務隔離 （知識庫文章）](http://support.microsoft.com/kb/2620201)   
 [存取 Token (MSDN)](/windows/desktop/SecAuthZ/access-tokens)   
 [安全性識別碼 (MSDN)](/windows/desktop/SecAuthZ/security-identifiers)   
 [存取 Token (Wikipedia)](http://en.wikipedia.org/wiki/Access_token)   
 [存取控制清單 (Wikipedia)](http://en.wikipedia.org/wiki/Access_control_list)  
  
  
