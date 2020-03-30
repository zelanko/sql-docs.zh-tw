---
title: 資料庫屬性 (鏡像頁面) | Microsoft 文件
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.mirroring.f1
ms.assetid: 5bdcd20f-532d-4ee6-b2c7-18dbb7584a87
author: stevestein
ms.author: sstein
ms.openlocfilehash: a25b2b40b147cd0bd23e8c7554e548b6a577d539
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68099589"
---
# <a name="database-properties-mirroring-page"></a>資料庫屬性 (鏡像頁面)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  請從主體資料庫存取此頁面，並且用它來設定和修改資料庫的資料庫鏡像屬性。 您也可以用來它啟動「設定資料庫鏡像安全性精靈」，以便檢視鏡像工作階段的狀態，以及暫停或移除資料庫鏡像工作階段。  
  
> **重要！！！** 啟動鏡像前必須先設定安全性。 如果還沒有啟動鏡像，則必須使用精靈來開始。 在精靈完成之前，[鏡像]  頁面的文字方塊都是停用狀態。  
  
 **使用 SQL Server Management Studio 設定資料庫鏡像**  
  
-   [使用 Windows 驗證建立資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="options"></a>選項。  
 **設定安全性**  
 按一下這個按鈕即可啟動 [設定資料庫鏡像安全性精靈]  。  
  
 如果精靈成功完成，則會根據鏡像是否已開始來決定採取的動作，如下所示：  
  
|||  
|-|-|  
|如果鏡像尚未開始。|屬性頁面會快取該連接資訊，同時也會快取表示鏡像資料庫是否有夥伴屬性集的值。<br /><br /> 在精靈結束時，會提示您使用預設的伺服器網路位址和作業模式來啟動資料庫鏡像。 如果您需要變更網路位址或作業模式，請按一下 [不要啟動鏡像]  。|  
|如果鏡像已經開始。|如果在精靈中變更了見證伺服器，設定就會隨之變更。|  
  
 **伺服器網路位址**  
 下列每個伺服器執行個體都有一個相等的選項：[主體]  、[鏡像]  和 [見證]  。  
  
 伺服器執行個體的伺服器網路位址，是在您完成「設定資料庫鏡像安全性精靈」時自動指定的。 完成精靈之後，如有必要，可以再用手動方式修改網路位址。  
  
 伺服器網路位址具有以下基本語法：  
  
 TCP **://** _fully_qualified_domain_name_ **:** _port_  
  
 其中  
  
-   *fully_qualified_domain_name* 是伺服器執行個體所在的伺服器。  
  
-   *port* 是指派給伺服器執行個體資料庫鏡像端點的通訊埠。  
  
     若要參與資料庫鏡像，伺服器需要有資料庫鏡像端點。 當您使用「設定資料庫鏡像安全性精靈」建立伺服器執行個體的第一個鏡像工作階段時，精靈就會自動建立端點，並且設定其使用「Windows 驗證」。 如需如何使用憑證型驗證精靈的相關資訊，請參閱 [使用 Windows 驗證建立資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)。  
  
    >**重要！！**  每個伺服器執行個體需要一個並只有一個資料庫鏡像端點，無論要支援的鏡像工作階段數目為多少。  
  
 例如，如果是在名稱為 `DBSERVER9` 之電腦系統上、其端點使用通訊埠 `7022`的伺服器執行個體，則其網路位址可能是：  
  
```  
TCP://DBSERVER9.COMPANYINFO.ADVENTURE-WORKS.COM:7022  
```  
  
 如需詳細資訊，請參閱 [指定伺服器網路位址 &#40;資料庫鏡像&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)。  
  
> **注意：** 資料庫鏡像工作階段期間，無法變更主體和鏡像伺服器執行個體；不過，在工作階段期間可以變更見證伺服器執行個體。 如需詳細資訊，請參閱此主題稍後的「備註」。  
  
 **啟動鏡像**  
 當所有下列條件都存在時，按一下即可開始鏡像：  
  
-   鏡像資料庫必須存在。  
  
     必須使用 WITH NORECOVERY 還原主體資料庫最近的完整備份 (有時也需要記錄檔備份) 的方式，在鏡像伺服器上建立鏡像資料庫，才能啟動鏡像。 如需詳細資訊，請參閱 [準備鏡像資料庫以進行鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)。  
  
-   已經指定主體和鏡像伺服器執行個體的 TCP 位址 (在 [伺服器網路位址]  區段中)。  
  
-   如果將作業模式設定為 [具有自動容錯移轉的高安全性 (同步)]，則也要指定鏡像伺服器執行個體的 TCP 位址。  
  
-   安全性已正確設定。  
  
 按一下 [啟動鏡像]  以起始工作階段。 Database Engine 會嘗試自動連接到鏡像夥伴，以確認鏡像伺服器已正確設定，並開始鏡像工作階段。 如果可以啟動鏡像，就會建立一個作業來監視資料庫。  
  
 **暫停** 或 **繼續**  
 在資料庫鏡像工作階段期間，按一下 [暫停]  即可暫停工作階段。 會出現提示字元要求確認；如果您按一下 **[是]** ，工作階段將暫停，然後按鈕將變更為 **[繼續]** 。 若要繼續工作階段，請按一下 **[繼續]** 。  
  
 如需暫停工作階段之影響的相關資訊，請參閱 [暫停與繼續資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)。  
  
> **重要！！** 在強制服務之後，當原始主體伺服器重新連接時，會暫停鏡像。 在這種情況下繼續執行鏡像，很可能會造成原始主體伺服器上的資料遺失。 如需如何管理潛在資料遺失的相關資訊，請參閱 [資料庫鏡像工作階段期間的角色切換 &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)。  
  
 **移除鏡像**  
 在主體伺服器執行個體上，按一下即可停止工作階段並從資料庫中移除鏡像組態。 此時會出現要求確認的提示；如果您按一下 [是]  ，就會停止工作階段並移除鏡像。 如需移除資料庫鏡像之影響的相關資訊，請參閱 [移除資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)。  
  
> **注意：** 如果這是伺服器執行個體上的唯一鏡像資料庫，便會移除監視作業。  
  
 **容錯移轉**  
 按一下即可以手動方式將主體資料庫容錯移轉至鏡像資料庫。  
  
> **注意：** 如果鏡像工作階段是在高效能模式中執行，則不支援手動容錯移轉。 若要以手動方式容錯移轉，必須先將作業模式變更為 [不具有自動容錯移轉的高安全性 (同步)]  。 在容錯移轉完成之後，就可以將新的主體伺服器執行個體上的作業模式再變回 [高效能 (非同步)]  。  
  
 會出現提示要求確認。 如果您按一下 [是]  ，系統就會嘗試容錯移轉。 主體伺服器一開始會使用 Windows 驗證來嘗試連接至鏡像伺服器。 如果 Windows 驗證沒有用，主體伺服器就會顯示 [連接到伺服器]  對話方塊。 如果鏡像伺服器使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請在 [驗證]  方塊中選取 [SQL Server 驗證]  。 在 [登入]  文字方塊中，指定要用來連接至鏡像伺服器的登入帳戶，然後在 [密碼]  文字方塊中，指定該帳戶的密碼。  
  
 如果容錯移轉成功，[資料庫屬性]  對話方塊就會關閉。 主體和鏡像伺服器角色會相互切換：先前的鏡像資料庫變成主體資料庫，而先前的主體資料庫則變成鏡像資料庫。 請注意，舊的主體資料庫上的 [資料庫屬性]  對話方塊會立即變成無法使用，因為它已經變成鏡像資料庫；而在容錯移轉之後，就可以在新的主體資料庫上使用此對話方塊。  
  
 如果容錯移轉失敗，則會顯示錯誤訊息，而且對話方塊會保持開啟狀態。  
  
> **重要！！** 修改 [資料庫屬性]  對話方塊中的屬性後，如果您按一下 [容錯移轉]  ，就會失去這些變更。 若要儲存目前的變更，請對確認提示回答 [否]  ，然後按一下 [確定]  以儲存變更。 接著，重新開啟 [資料庫屬性] 對話方塊並按一下 [容錯移轉]  。  
  
 **作業模式**  
 選擇性地變更作業模式。 某些作業模式的可用性取決於是否有為見證指定 TCP 位址。 選項如下：  
  
|選項|見證？|說明|  
|------------|--------------|-----------------|  
|**高效能 (非同步)**|Null (若存在，則不使用，但工作階段需要仲裁)|為了將效能發揮到極致，鏡像資料庫的狀態總是會比主體資料庫有些延遲，永遠無法真正的同步。 然而，在資料庫之間的間距通常很小。 夥伴的遺失將具有下列結果：<br /><br /> 如果鏡像伺服器執行個體已無法使用，主體將繼續。<br /><br /> 如果主體伺服器執行個體變成無法使用，鏡像就會停止。 但是如果工作階段沒有見證 (依照建議)，或者見證已連接到鏡像伺服器，則鏡像伺服器會以暖待命方式保持可存取狀態；資料庫擁有者可以對鏡像伺服器執行個體強制服務 (有遺失資料的可能)。|  
|**不具有自動容錯移轉的高安全性 (同步)**|否|保證會將所有已認可的交易都寫入鏡像伺服器上的磁碟。<br /><br /> 夥伴互相連接時才可以執行手動容錯移轉。<br /><br /> 夥伴的遺失將具有下列結果：<br /><br /> 如果鏡像伺服器執行個體已無法使用，主體將繼續。<br /><br /> 如果主體伺服器執行個體變成無法使用，鏡像就會停止，但是會以暖待命方式保持可使用狀態；資料庫擁有者可以對鏡像伺服器執行個體強制服務 (有遺失資料的可能)。|  
|**具有自動容錯移轉的高安全性 (同步)**|是 (必要)|藉由納入見證伺服器執行個體來支援自動容錯移轉，而發揮最大的可用性。 請注意，您必須先指定見證伺服器位址，才能選取 **[具有自動容錯移轉的高安全性 (同步)]** 選項。<br /><br /> 每當夥伴互相連接時才可以執行手動容錯移轉。<br /><br /> **&#42;&#42; 重要事項 &#42;&#42;** 如果見證中斷連線，則必須將夥伴相互連線，才能使用資料庫。 如需詳細資訊，請參閱[仲裁：見證如何影響資料庫可用性 &#40;資料庫鏡像&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)。<br /><br /> 在同步作業模式中，保證會將所有已認可的交易都寫入鏡像伺服器上的磁碟。 在有見證的情況下，夥伴的遺失將具有下列結果：<br /><br /> 如果主體伺服器執行個體已無法使用，將發生自動容錯移轉。 鏡像伺服器執行個體將切換到主體的角色，並且提供它的資料庫做為主體資料庫。<br /><br /> 如果鏡像伺服器執行個體已無法使用，主體將繼續。<br /><br /> <br /><br /> 如需詳細資訊，請參閱 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)。|  
  
 在鏡像開始後，您可以變更作業模式，並且按一下 **[確定]** 以儲存變更。  
  
 如需作業模式的詳細資訊，請參閱 [資料庫鏡像作業模式](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)。  
  
 **狀態**  
 鏡像開始之後，當您選取 [鏡像]  頁面，[狀態]  面板會顯示資料庫鏡像工作階段的狀態。 若要更新 [狀態]  面板，請按一下 [重新整理]  按鈕。 可能的狀態如下：  
  
|狀態|說明|  
|------------|-----------------|  
|**這個資料庫尚未設定鏡像**|資料庫鏡像工作階段不存在，並且在 [鏡像]  頁面上沒有可以報告的活動。|  
|**已暫停**|主體資料庫可供使用，但是不會將任何記錄傳送到鏡像伺服器。|  
|**沒有連接**|主體伺服器執行個體無法連接到其夥伴。|  
|**正在同步處理**|鏡像資料庫的內容落後於主體資料庫的內容。 主體伺服器執行個體正在將記錄傳送到鏡像伺服器執行個體，這時會將變更套用至鏡像資料庫，以便向前復原。<br /><br /> 在資料庫鏡像工作階段開始時，鏡像資料庫和主體資料庫都是處於這個狀態。|  
|**容錯移轉**|在主體伺服器執行個體上，手動容錯移轉 (角色切換) 已經開始，而且伺服器目前正在轉換成鏡像角色。 在這個狀態下，使用者與主體資料庫的連接會快速結束，而且接著資料庫就會立即接替鏡像角色。|  
|**已同步處理**|當鏡像伺服器足以追趕上主體伺服器時，資料庫狀態就會變成 [已同步處理]  。 只要主體伺服器繼續傳送變更到鏡像伺服器，而鏡像伺服器也繼續將變更套用到鏡像資料庫，資料庫便會保持在這種狀態。<br /><br /> 在高安全性模式中，可以進行容錯移轉，不會遺失任何資料。<br /><br /> 在高效能模式中，永遠都有可能遺失部分資料，即使是在 [已同步處理]  狀態也是如此。|  
  
 如需詳細資訊，請參閱[鏡像狀態 &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)。  
  
 **[重新整理]**  
 按一下以更新 [狀態]  方塊。  
  
## <a name="remarks"></a>備註  
 如不熟悉資料庫鏡像，請參閱 [資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
### <a name="adding-a-witness-to-an-existing-session"></a>將見證加入至現有的工作階段  
 您可以將見證加入至現有的工作階段，或是取代現有的見證。 如果您知道見證的伺服器網路位址，可以用手動方式將其輸入至 [見證]  欄位。 如果您不知道見證的伺服器網路位址，則請使用「設定資料庫鏡像安全性精靈」來設定見證。 將位址輸入至該欄位之後，請確定已選取 [具有自動容錯移轉的高安全性 (同步)]  選項。  
  
 設定新的見證之後，必須按一下 [確定]  才能將其加入至鏡像工作階段。  
  
 **若要在使用 Windows 驗證時加入見證**  
  
 [新增或取代資料庫鏡像見證 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
### <a name="removing-a-witness"></a>移除見證  
 若要移除見證，請從 [見證]  欄位中刪除其伺服器網路位址。 如果從具有自動容錯移轉的高安全性模式切換到高效能模式，則會自動清除 [見證]  欄位。  
  
 在刪除見證之後，必須按一下 [確定]  才能將其從鏡像工作階段中移除。  
  
### <a name="monitoring-database-mirroring"></a>監視資料庫鏡像  
 若要監視伺服器執行個體上的鏡像資料庫，可以使用資料庫鏡像監視器或 sp_dbmmonitorresults 系統預存程序。  
  
 **若要監視鏡像資料庫**  
  
-   [啟動資料庫鏡像監視器 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
 如需詳細資訊，請參閱 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [指定伺服器網路位址 &#40;資料庫鏡像&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [使用 Windows 驗證建立資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [啟動資料庫鏡像監視器 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像和 Always On 可用性群組的傳輸安全性 &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [資料庫鏡像工作階段期間的角色切換 &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [暫停與繼續資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)   
 [移除資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [資料庫鏡像見證](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
