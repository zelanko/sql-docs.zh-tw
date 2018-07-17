---
title: 發行集屬性，FTP 快照集和網際網路 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.internetsynchronization.f1
ms.assetid: 8e0198c3-5e4e-418c-9920-78ccbbfc1323
caps.latest.revision: 25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99012d771ff9dcaa3f71c13d35ee730e3e5d15fb
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37351660"
---
# <a name="publication-properties-ftp-snapshot-and-internet"></a>發行集屬性，FTP 快照集和網際網路
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此頁面可以讓您：  
  
-   設定屬性以經由檔案傳輸通訊協定 (File Transfer Protocol，FTP) 傳遞快照集。 如需詳細資訊，請參閱[透過 FTP 傳送快照集](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。 若要使用 FTP 傳遞快照集，您必須設定 FTP 伺服器。 請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 文件集以取得詳細資訊。  
  
    > [!NOTE]  
    >  FTP 設定若有任何變更，就需要產生新的快照集。  
  
-   針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本上的合併式複寫，設定 Web 同步處理的屬性，即可讓訂閱透過 HTTPS (安全超文字傳輸通訊協定) 進行同步處理。 若要使用 Web 同步處理，您必須設定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 伺服器。 如需詳細資訊，請參閱＜ [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)＞。  
  
## <a name="options"></a>選項。  
 **透過 FTP 存取快照集檔案**  
 選取 **[允許訂閱者使用 FTP (檔案傳輸通訊協定) 下載快照集檔案]**，並指定 **[FTP 伺服器名稱]**、 **[通訊埠編號]**、 **[FTP 根資料夾的路徑]**、 **[登入]** 和 **[密碼]**，即可讓訂閱者使用 FTP 傳遞快照集。  
  
 此選項可以讓訂閱者使用 FTP 擷取快照集檔案，但這並不是必要的。 如果您選取此選項，新增訂閱精靈就會預設讓訂閱者經由 FTP 擷取快照集檔案。 若要變更此設定，請使用 **[訂閱屬性]** 對話方塊。 如果您讓訂閱者經由 FTP 存取快照集檔案，請在 **[快照集屬性]** 對話方塊的 **[快照集]** 頁面上，指定 FTP 資料夾作為快照集檔案的位置。 這樣做會在新的快照集產生時，讓快照集代理程式自動更新 FTP 資料夾中的檔案。 如果位置沒有設定到 FTP 資料夾，當新的快照集產生時，您就必須手動更新檔案。 如需詳細資訊，請參閱[透過 FTP 傳遞快照集](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)。  
  
 **Web 同步處理**  
 僅限合併式複寫。 選取 **[允許訂閱者連接到 Web 伺服器進行同步處理]**，並指定 Web 伺服器位址讓合併式訂閱者使用 Web 同步處理。 Web 伺服器必須使用安全通訊端層 (SSL)，且網址必須完整，例如 `https://server.domain.com/synchronize`。 如需詳細資訊，請參閱 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [檢視及修改發送訂閱屬性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
