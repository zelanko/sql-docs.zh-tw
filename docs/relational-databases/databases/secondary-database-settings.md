---
title: 次要資料庫設定 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.logshipping.settings.dest.f1
ms.assetid: f992ffc9-ee42-43fe-acec-512032f0ded1
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 45eb465a92fcb10b49ea68dbefa59454332c3b58
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="secondary-database-settings"></a>次要資料庫設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以使用此對話方塊，來設定和修改記錄傳送組態中，次要資料庫的屬性。  
  
 如需記錄傳送概念的說明，請參閱 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。  
  
## <a name="options"></a>選項。  
 **次要伺服器執行個體**  
 顯示目前在記錄傳送組態中設定為次要伺服器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。  
  
 **次要資料庫**  
 顯示記錄傳送組態中，次要資料庫的名稱。 將新的次要資料庫加入記錄傳送組態時，您可以從清單中選擇資料庫，或在方塊中輸入新資料庫的名稱。 如果您輸入新資料庫的名稱，就必須選取 **[初始化]** 索引標籤上的選項，將主要資料庫的完整資料庫備份還原至次要資料庫中。 進行還原作業時，會建立新的資料庫。  
  
 **[連接]**  
 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，在記錄傳送組態中做為次要伺服器使用。 用來連接的帳戶必須是次要伺服器執行個體上的系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
 **初始化索引標籤**  
 選項如下：  
  
 **是，產生主要資料庫的完整備份，並將其還原到次要資料庫**  
 透過備份主要資料庫並將它還原至次要伺服器，即可讓 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 設定您的次要資料庫。 如果您在 **[次要資料庫]** 方塊中輸入新的資料庫名稱，進行還原作業時就會建立此資料庫。  
  
 **還原選項**  
 如果您要將次要資料庫的資料與記錄檔，還原至次要伺服器的非預設位置，請按一下此選項。  
  
 此按鈕會開啟 **[還原選項]** 對話方塊。 因此，您可以指定非預設資料夾的路徑，以存放次要資料庫及其記錄。 如果您指定其中一個資料夾，就必須同時指定兩者。  
  
 這些路徑必須參考到次要伺服器的本機磁碟機。 而且這些路徑必須有本機磁碟機代號和冒號 (例如 `C:`)。 對應的磁碟機代號或網路路徑無效。  
  
 如果您按一下 **[還原選項]** 按鈕，然後決定要使用預設資料夾，我們建議您取消 **[還原選項]** 對話方塊。 若您已經指定非預設位置，而想要改用預設位置，請再按一下 **[還原選項]** ，並清除文字方塊，然後按一下 [確定]。  
  
 **是，將主要資料庫的現有備份還原到次要資料庫**  
 讓 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 使用主要資料庫的現有備份，以初始化次要資料庫。 在 **[備份檔案]** 方塊中輸入該備份的位置。 如果您在 [次要資料庫] 方塊中輸入新的資料庫名稱，進行還原作業時就會建立此資料庫。  
  
 **[備份檔案]**  
 如果您選擇 [是，將主要資料庫的現有備份還原到次要資料庫] 選項，請輸入要用來初始化次要資料庫之完整資料庫備份的路徑與檔案名稱。  
  
 **還原選項**  
 請參閱本主題稍早有關此按鈕的描述。  
  
 **否，次要資料庫已初始化**  
 指定次要資料庫已經初始化，且已備妥要從主要資料庫接受交易記錄的備份。 如果您在 **[次要資料庫]** 方塊中輸入新的資料庫名稱，就無法使用此選項。  
  
 **複製檔案索引標籤**  
 選項如下：  
  
 **複製之檔案的目的資料夾**  
 輸入還原至次要資料庫時，應該用來複製交易記錄備份的路徑。 通常它是次要伺服器上之資料夾的本機路徑。 不過，如果此資料夾位於另一個伺服器上，您就必須指定此資料夾的 UNC 路徑。 次要伺服器執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶，必須擁有此資料夾的讀取權限。 您也必須授與此網路共用的讀取與寫入權限給 Proxy 帳戶，Proxy 帳戶才能在次要伺服器執行個體上執行複製與還原作業。 根據預設，這是次要伺服器執行個體的 SQL Server Agent 服務帳戶，但是系統管理員 (sysadmin) 可以為此作業選擇其他 Proxy 帳戶。  
  
 **在此時間後刪除複製的檔案**  
 選擇所複製的交易記錄備份在被刪除之前，要在目的資料夾中存在多久。  
  
 **作業名稱**  
 顯示用以將交易記錄備份檔案，從主要伺服器複製至次要伺服器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業名稱。 第一次建立此作業時，您可以在方塊中輸入新的名稱。  
  
 **[排程]**  
 顯示用來從主要伺服器複製交易記錄備份至次要伺服器的 SQL Server Agent 複製作業的目前排程。 按一下 **[排程...]**，即可修改此排程。  
  
 **[排程...]**  
 修改用來從主要伺服器複製交易記錄備份至次要伺服器的 SQL Server Agent 作業的參數。  
  
 **停用此作業**  
 暫停 SQL Server Agent 複製作業。  
  
 **還原交易記錄索引標籤**  
 選項如下：  
  
 **還原備份時，中斷連接資料庫中的使用者**  
 正在還原交易記錄備份時，自動中斷連接次要資料庫的使用者。  
  
 **不復原模式**  
 讓次要資料庫維持 NORECOVERY 模式。  
  
 **待命模式**  
 讓次要資料庫維持 STANDBY 模式。 此模式僅允許針對資料庫執行唯讀作業。  
  
> [!IMPORTANT]  
>  例如，如果將現有的次要資料庫的復原模式從 [不復原模式] 變更為 [待命模式]，則該變更只有在下次記錄備份還原到資料庫之後才會生效。  
  
 **延遲還原備份至少**  
 選擇還原交易記錄備份至次要資料庫的延遲 (如果有的話)。  
  
 **如果未在此時間內進行還原，則發出警示**  
 選擇在發出未發生交易記錄還原的警示之前，記錄傳送等候的時間量。  
  
 **作業名稱**  
 顯示用來還原交易記錄備份至次要資料庫的 SQL Server Agent 作業的名稱。 第一次建立此作業時，您可以在方塊中輸入新的名稱。  
  
 **[排程]**  
 顯示用來還原交易記錄備份至次要資料庫的 SQL Server Agent 作業的目前排程。 按一下 **[排程...]**，即可修改此選項。  
  
 **[排程...]**  
 修改與 SQL Server Agent 還原作業相關的參數。  
  
 **停用此作業**  
 暫停次要資料庫的還原作業。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  
