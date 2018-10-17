---
title: 使用複製資料庫精靈 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.cdw.transfermethod.f1
- sql12.swb.cdw.welcome.f1
- sql12.swb.cdw.packageconfiguration.f1
- sql12.swb.cdw.schedule.f1
- sql12.swb.cdw.destination.f1
- sql12.swb.cdw.complete.f1
- sql12.swb.cdw.destinationconfiguration.f1
- sql12.swb.cdw.selectdatabaseobjects.f1
- sql12.swb.cdw.databases.f1
- sql12.swb.cdw.source.f1
- sql12.swb.cdw.locationofsourcedbfiles.f1
helpviewer_keywords:
- Copy Database Wizard
- starting Copy Database Wizard
ms.assetid: 7a999fc7-0a26-4a0d-9eeb-db6fc794f3cb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2d47f2e7ce32ef77ec7188efbc7c09d053cf8208
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108688"
---
# <a name="use-the-copy-database-wizard"></a>使用複製資料庫精靈
  「複製資料庫精靈」可讓您輕鬆地在伺服器之間移動或複製資料庫及其物件，而不需要讓伺服器停機。 您也可以從舊版升級的資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 使用此精靈可以執行下列作業：  
  
-   挑選來源和目的地伺服器。  
  
-   選取要移動、複製或升級的資料庫。  
  
-   為資料庫指定檔案位置。  
  
-   在目的地伺服器上建立登入。  
  
-   複製其他支援的物件、作業、使用者定義的預存程序和錯誤訊息。  
  
-   何時要移動或複製資料庫的排程。  
  
 除了複製資料庫以外，您還可以複製相關的中繼資料，例如，被複製之資料庫所需之 **master** 資料庫中的登入和物件。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [必要條件](#Prerequisites)  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **使用複製資料庫精靈用於：**  
  
     [複製、 移動或升級資料庫](#Copy_Move)  
  
-   **待處理，在升級之後：**  
  
     [升級 SQL Server 資料庫之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   Express 版本不提供複製資料庫精靈。  
  
-   複製資料庫精靈無法用於複製或移動下列資料庫。  
  
    -   系統資料庫  
  
    -   要用於複寫的資料庫。  
  
    -   標示為「無法存取」、「正在載入」、「離線」、「正在復原」、「有疑問」或是「緊急模式」的資料庫。  
  
-   資料庫升級後，無法降級至舊版。  
  
-   若您選取 **[移動]** 選項，則當移動資料庫之後，精靈會自動刪除來源資料庫。 如果您選取 **[複製]** 選項，「複製資料庫精靈」就不會刪除來源資料庫。  
  
-   如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件方法來移動全文檢索目錄，您必須在移動之後重新擴展索引。  
  
-   卸離和附加方法可卸離資料庫、移動或複製資料庫 .mdf、.ndf 和 .ldf 檔案，並在新的位置中重新附加資料庫。 對於卸離和附加方法而言，為了避免資料遺失或不一致，使用中工作階段不能附加到正在移動或複製的資料庫。 如果有任何使用中工作階段存在，「複製資料庫精靈」將不會執行移動或複製作業。 對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件方法而言，因為資料庫絕對不會離線，所以允許使用中工作階段。  
  
###  <a name="Prerequisites"></a> 必要條件  
 確定目的地伺服器上已啟動 SQL Server Agent。  
  
###  <a name="Recommendations"></a> 建議  
  
-   為了確保升級的資料庫能有最佳效能，請針對升級的資料庫執行 sp_updatestats (更新統計資料)。  
  
-   將資料庫複製到另一個伺服器執行個體時，為了提供一致的經驗給使用者和應用程式，您可能會需要在其他伺服器執行個體上為資料庫重新建立部分或所有中繼資料，例如登入和作業。 如需詳細資訊，請參閱 [在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須在來源伺服器與目的地伺服器上成為 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
##  <a name="Copy_Move"></a> 複製、 移動或升級資料庫  
  
1.  在  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，請在物件總管] 中展開**資料庫**，以滑鼠右鍵按一下資料庫，指向**工作**，然後按一下 **複製資料庫**。  
  
2.  從 **[選取來源伺服器]** 頁面，指定要移動或複製之資料庫所在的伺服器，以及輸入登入資訊。 在您選取驗證方法並輸入登入資訊之後，按 **[下一步]** 以建立與來源伺服器的連接。 在整個工作階段中，此連接會保持開啟。  
  
     **來源伺服器**  
     選取您想要移動或複製之資料庫所在的伺服器名稱，或是按一下瀏覽 (**...**) 按鈕，尋找您要的伺服器。 該伺服器必須至少為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。  
  
     **[使用 Windows 驗證]**  
     可讓使用者透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者帳戶連接。  
  
     **[使用 SQL Server 驗證]**  
     允許使用者藉由提供連線[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證使用者名稱和密碼。  
  
     **使用者名稱**  
     輸入要用來連接的使用者名稱。 此選項才可使用您選取要使用連線[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。  
  
     **密碼**  
     輸入登入的密碼。 這個選項只有在您選取了使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接時才可以使用。  
  
     **下一個**  
     連接到伺服器，並驗證使用者。 此處理序會檢查使用者是否為所選取電腦中的 **[系統管理員 (sysadmin)]** 固定伺服器角色成員。  
  
3.  從 **[選取目的地伺服器]** 頁面，指定將移動或複製資料庫的伺服器。 如果您將來源和目的地伺服器設定成同一個伺服器執行個體，您就會複製一個資料庫。 在這種情況下，您必須稍後在精靈中重新命名此資料庫。 只有當目的地伺服器上沒有名稱衝突時，才可以將來源資料庫名稱用於複製或移動的資料庫。 如果有名稱衝突存在，您必須先手動解決目的地伺服器上的衝突，然後才能在這裡使用來源資料庫名稱。  
  
     **目的地伺服器**  
     選取要移動或複製資料庫的目的地伺服器名稱，或按一下瀏覽 (**...**) 按鈕來尋找目的地伺服器。  
  
    > [!NOTE]  
    >  您可以使用屬於叢集伺服器的目的地。「複製資料庫精靈」將會確保您只能選取叢集目的地伺服器上的共用磁碟機。  
  
     **[使用 Windows 驗證]**  
     可讓使用者透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者帳戶連接。  
  
     **[使用 SQL Server 驗證]**  
     允許使用者藉由提供連線[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證使用者名稱和密碼。  
  
     **使用者名稱**  
     輸入要用來連接的使用者名稱。 此選項才可使用您已選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。  
  
     **密碼**  
     輸入登入的密碼。 此選項才可使用您已選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。  
  
     **下一個**  
     連接到伺服器，並驗證使用者。 此處理序會檢查使用者在選取的電腦上是否擁有以上所列的權限。  
  
4.  從 **[選取傳送方法]** 頁面，選取傳送方法。  
  
     **使用卸離和附加方法**  
     從來源伺服器卸離資料庫，將資料庫檔案 (.mdf、.ndf 以及 .ldf) 複製到目的地伺服器，然後在目的地伺服器端附加該資料庫。 此方法通常是比較快速的方法，因為它的主要工作是讀取來源磁碟和寫入目的地磁碟。 不需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 邏輯在資料庫中建立物件，或建立資料儲存結構。 不過，如果資料庫包含大量已配置但未使用的空間，此方法就會比較慢。 例如，新的且實際上幾乎是空的資料庫，在建立時若配置 100 MB，即使資料只填滿 5 MB，也會複製全部 100 MB。  
  
    > [!NOTE]  
    >  此方法讓使用者在傳送期間無法使用資料庫。  
  
     **如果失敗，則重新附加來源資料庫**  
     複製資料庫時，一律會將原始資料庫檔案重新附加至來源伺服器。 無法完成資料庫移動時，使用這個方塊即可將原始檔案重新附加至來源資料庫。  
  
     **使用 SQL 管理物件方法**  
     這個方法會讀取來源資料庫上的每個資料庫物件的定義，然後在目的地資料庫中建立每個物件。 接著它會從來源資料表傳送資料到目的地資料表，重新建立索引與中繼資料。  
  
    > [!NOTE]  
    >  在傳送期間，資料庫使用者可以繼續存取資料庫。  
  
5.  從 **[選取資料庫]** 頁面，選取您要從來源伺服器，移動或複製到目的地伺服器的資料庫。 請參閱本主題中＜開始之前＞一節的＜ [限制事項](#Restrictions) ＞。  
  
     **[移動]**  
     移動資料庫至目的地伺服器。  
  
     **[複製]**  
     複製資料庫至目的地伺服器。  
  
     **Source**  
     顯示存在於來源伺服器上的資料庫。  
  
     **狀態**  
     如果可以移動資料庫，就會顯示 **[確定]** 。 否則就會顯示無法移動資料庫的原因。  
  
     **[重新整理]**  
     重新整理資料庫清單。  
  
     **下一個**  
     開始驗證處理，然後移動到下一個畫面。  
  
6.  從 **[設定目的地資料庫]** 頁面，適當地變更資料庫名稱，以及指定資料庫檔案的位置和名稱。 每次移動或複製各個資料庫時，就會出現此頁面。  
  
7.  從 **[選取資料庫物件]** 頁面，選取要包含在移動或複製作業中的物件。 此頁面只能在來源和目的地是不同的伺服器時使用。 若要包含物件，請按一下 [可用的相關物件] 方塊中的物件名稱，然後按一下 [>>] 按鈕，將物件移至 [選取的相關物件] 方塊。 若要排除物件，請按一下 [選取的相關物件] 方塊中的物件名稱，然後按一下 [<\<] 按鈕，將物件移至 [可用的相關物件] 方塊。 根據預設，屬於所選取類型的所有物件都會傳送。 若要選擇任何類型的個別物件，請按一下 **[選取的相關物件]** 方塊中之任何物件類型旁的省略符號按鈕。 這會開啟一個對話方塊，其中您可以選取個別物件。  
  
     **登入 （在執行階段的所有登入）**  
     在移動或複製作業中加入登入。 依預設為已選取。  
  
     **master 資料庫裡的預存程序**  
     將 **master** 資料庫裡的預存程序包含在移動或複製作業中。  
  
    > [!NOTE]  
    >  擴充預存程序及其相關聯的 DLL 不適合自動複製。  
  
     **SQL Server Agent 作業**  
     將 **msdb** 資料庫裡的作業包含在移動或複製作業中。  
  
     **使用者自訂錯誤訊息**  
     將使用者自訂錯誤訊息包含在移動或複製作業中。  
  
     **端點**  
     包含在來源資料庫中所定義的端點。  
  
     **全文檢索目錄**  
     包含來源資料庫中的全文檢索目錄。  
  
     **SSIS 封裝**  
     包含在來源資料庫中所定義的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝。  
  
     **說明**  
     對物件的描述。  
  
8.  從 **[來源資料庫檔案的位置]** 頁面，指定包含來源伺服器資料庫檔案的檔案系統共用。 如果來源和目的地伺服器執行個體位於不同的電腦上，這就是必要項。  
  
     **[資料庫備份]**  
     顯示要移動的每個資料庫的名稱。  
  
     **資料夾位置**  
     指定檔案系統上之來源資料庫檔案的位置。  
  
     例如：C:\Program Files\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\DATA  
  
     **來源伺服器上的檔案共用**  
     將來源資料庫檔案的位置指定為檔案共用的路徑。  
  
     例如:"\\\\*server_name*\C$\Program Files\Microsoft SQL Server\MSSQL110。MSSQLSERVER\MSSQL\Data  
  
9. 複製資料庫精靈會建立[!INCLUDE[ssIS](../../includes/ssis-md.md)]封裝來傳送資料庫。 請從**設定套件**頁面適當地自訂封裝。  
  
     **封裝位置**  
     顯示 where[!INCLUDE[ssIS](../../includes/ssis-md.md)]封裝的寫入。  
  
     **封裝名稱**  
     輸入的名稱[!INCLUDE[ssIS](../../includes/ssis-md.md)]封裝。  
  
     **記錄選項**  
     選取是要將記錄資訊儲存在 Windows 事件記錄檔中，還是儲存在文字檔中。  
  
     **錯誤記錄檔路徑**  
     提供記錄檔位置的路徑。 只有在已選取文字檔案登入選項時，才能使用此選項。  
  
10. 從 **[排程封裝]** 頁面，指定您要讓移動或複製作業開始的時間。 如果您不是系統管理員，您必須指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent Proxy 帳戶可存取[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)](SSIS) 封裝執行子系統。  
  
     **Run immediately**  
     在您按 **[下一步]** 之後，開始移動或複製作業。  
  
     **[排程]**  
     稍後開始移動或複製作業。 目前的排程設定會出現在描述方塊中。 若要變更排程，請按一下 **[變更]**。  
  
     **變更**  
     開啟 **[新增作業排程]** 對話方塊。  
  
     **Integration Services proxy 帳戶**  
     選取可用的 Proxy 帳戶。 若要排程傳送，至少必須有一個 Proxy 帳戶可供使用者使用，而且帳戶要設定為擁有 **[SQL Server Integration Services 封裝執行]** 子系統的權限。  
  
     若要建立的 proxy 帳戶[!INCLUDE[ssIS](../../includes/ssis-md.md)]封裝執行，在 [物件總管] 中，展開**SQL Server Agent**，展開**Proxy**，以滑鼠右鍵按一下**SSIS 套件執行**，然後按一下**新的 Proxy**。  
  
     **[系統管理員 (sysadmin)]** 固定伺服器角色成員的使用者，可以選取具有必要權限的 **[SQL Server Agent 服務帳戶]** 來執行這個作業步驟。  
  
11. 從 **[完成精靈]** 頁面，檢閱所選選項的摘要。 按 **[上一步]** 即可變更選項。 按一下 **[完成]** 以建立資料庫。 在傳送期間， **[正在執行作業]** 頁面會監視有關 **[複製資料庫精靈]** 執行的狀態資訊。  
  
     **動作**  
     列出每個執行的動作。  
  
     **狀態**  
     表示動作完全成功或失敗。  
  
     **Message**  
     提供每個步驟所傳回的任何訊息。  
  
##  <a name="FollowUp"></a> 待處理：升級 SQL Server 資料庫之後  
 在您使用複製資料庫精靈，將資料庫從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之後，資料庫就會變成立即可用並自動進行升級。 如果資料庫具有全文檢索索引，升級程序就會根據 **[全文檢索目錄升級選項]** 伺服器屬性的設定，匯入、重設或重建這些索引。 如果升級選項設定為 **[匯入]** 或 **[重建]**，則全文檢索索引在升級期間將無法使用。 根據進行索引的資料數量而定，匯入可能需要數個小時，而重建可能需要十倍以上的時間。 此外，請注意，當升級選項設定為 [匯入] 時，如果全文檢索目錄無法使用，系統就會重建相關聯的全文檢索索引。 如需有關檢視或變更 **全文檢索目錄升級選項** 屬性設定的詳細資訊，請參閱＜ [Manage and Monitor Full-Text Search for a Server Instance](../search/manage-and-monitor-full-text-search-for-a-server-instance.md)＞。  
  
 如果使用者資料庫的相容性層級在升級前為 100 或更高層級，則在升級後仍會保持相同。 如果已升級資料庫中的相容性層級為 90，則相容性層級會設定為 100 (這是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所支援的最低相容性層級)。 如需詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。  
  
## <a name="see-also"></a>另請參閱  
 [使用卸離與附加來升級資料庫 &#40;Transact-SQL&#41;](upgrade-a-database-using-detach-and-attach-transact-sql.md)   
 [建立 SQL Server Agent Proxy](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
  
