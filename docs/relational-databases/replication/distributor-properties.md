---
title: SQL Server 複寫散發者屬性對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configdistwizard.distdbproperties.f1
- sql13.rep.configdistwizard.distproperties.general.f1
- sql13.rep.configdistwizard.distproperties.publishers.f1
ms.assetid: f643c7c3-f238-4835-b81e-2c2b3b53b23f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2e58ef266f992911dc8360925649959b1aedd13f
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126613"
---
# <a name="sql-server-replication-distributor-properties-dialog-box"></a>SQL Server 複寫散發者屬性對話方塊 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本頁說明 [散發者屬性] 對話方塊內的頁面。 

## <a name="general"></a>一般
**[散發者屬性]** 對話方塊的 **[一般]** 頁面可讓您加入和刪除散發資料庫，以及設定散發資料庫屬性。  
  
 散發資料庫會儲存所有複寫類型的中繼資料和記錄資料，以及異動複寫的交易。 在許多情況下，單一散發資料庫即已足夠。 但是如果多個發行者使用單一散發者，請考慮為每個發行者建立散發資料庫。 這樣可以確保流經每個散發資料庫的資料都不同。  

 **資料庫**  
 **[資料庫]** 屬性方格會顯示散發者上之散發資料庫的名稱與保留屬性。 **[交易保留]** 是為異動複寫儲存交易的時間長度 (交易保留也稱為散發保留)。 **[記錄保留]** 是為所有的複寫類型儲存記錄中繼資料的時間長度。 如需散發保留的詳細資訊，請參閱[訂閱逾期與停用](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 按一下 **[資料庫]** 屬性方格中的屬性按鈕 ( **...** )，即可啟動 **[散發資料庫屬性]** 對話方塊。  
  
 **新增**  
 按一下即可建立新的散發資料庫。  
  
 **刪除**  
 在 **[資料庫]** 屬性方格中選取現有的散發資料庫，然後按一下 **[刪除]** 以刪除資料庫。 如果只有一個這種資料庫，就無法刪除此散發資料庫；每個散發者至少必須有一個散發資料庫。 若要刪除所有的散發資料庫，您必須停用電腦上的散發。 如需詳細資訊，請參閱[停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)。  
  
 **設定檔預設值**  
 按一下即可存取 **[代理程式設定檔]** 對話方塊中的複寫代理程式設定檔。 如需有關設定檔的詳細資訊，請參閱＜ [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)＞。  

## <a name="publishers"></a>[散發者屬性]
**[散發者屬性]** 對話方塊的 **[發行者]** 頁面可讓您啟用發行者，以使用此散發者。 您也可以設定與這些發行者相關聯的屬性。 請注意，讓發行者可以使用這個伺服器作為它的遠端散發者，並不會使該伺服器成為發行者。 您必須連接到發行者，設定其發行，並選擇此伺服器為散發者。 您可以透過新增發行集精靈來設定發行者和選擇散發者。  
  
 **發行者**  
 選取可使用這個散發者的伺服器。 按一下發行者旁的 [屬性] 按鈕 **(...)** ，以檢視和設定其他屬性。  
  
 **[加入]**  
 如果未列出您要允許的伺服器，請按一下 **[加入]** ，將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者或 Oracle 發行者加入可用發行者的清單中。 如果您加入的伺服器是第一部使用此散發者作為遠端散發者的伺服器，系統會提示您提供管理連結密碼。  
  
 **管理連結密碼**  
 使用 **distributor_admin** 登入進行發行者和遠端散發者的連接複寫時，這可用來指定或更新該連接複寫的密碼：  
  
-   如果散發者伺服器只是當成本機散發者，這個密碼會隨機產生並自動設定。   
-   如果散發者已經有遠端發行者，此頁面上或設定散發精靈的 **[散發者密碼]** 頁面上一開始就會提供密碼。    
-   如果啟用此散發者的第一個遠端發行者，系統會提示您輸入密碼。  如需散發者安全性的詳細資訊，請參閱[保護散發者](../../relational-databases/replication/security/secure-the-distributor.md)。  

## <a name="distribution-database"></a>散發資料庫 
 **[散發資料庫屬性]** 對話方塊可讓您檢視許多屬性，並設定資料庫的交易保留期限和記錄保留期限。  
  
 **名稱**  
 散發資料庫的名稱，預設為「distribution」(唯讀)。  
  
 **檔案位置**  
 資料庫檔案和記錄檔的位置 (唯讀)。  
  
 **交易保留期限**  
 又稱為散發保留期限。 交易的儲存時間長度，適用於異動複寫。 如需詳細資訊，請參閱 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 **記錄保留期限**  
 記錄中繼資料的儲存時間長度，適用於所有類型的複寫。  
  
 **佇列讀取器代理程式安全性**  
 佇列讀取器代理程式會用於具有佇列更新訂閱的異動複寫。 如果您在新增發行集精靈的 **[發行集類型]** 頁面上選取 **[具更新訂閱的交易式發行集]** ，則會自動建立佇列讀取器代理程式。 按一下 **[安全性設定]** ，即可變更執行代理程式和連接散發者的帳戶。  
  
 在此頁面上選取 **[建立佇列讀取器代理程式]** 也可以建立佇列讀取器代理程式 (如果已建立代理程式，此選項會停用)。  
  
 有兩個地方可以指定佇列讀取器代理程式的其他連接資訊：    
-   代理程式會使用 **[發行者屬性]** 對話方塊中指定的認證來連接發行者，該對話方塊可以從 **[散發者屬性]** 對話方塊的 **[發行者]** 頁面存取。    
-   代理程式會使用新增訂閱精靈中為散發代理程式指定的認證，來連接訂閱者。  如需詳細資訊，請參閱  [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。 
  
## <a name="see-also"></a>另請參閱  
 [[設定散發]](../../relational-databases/replication/configure-distribution.md)   
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
  
  
