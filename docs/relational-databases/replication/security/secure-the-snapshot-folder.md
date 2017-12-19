---
title: "保護快照集資料夾 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: snapshots [SQL Server replication], security
ms.assetid: 3cd877d1-ffb8-48fd-a72b-98eb948aad27
caps.latest.revision: "46"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7bfea98b84a87b9bd35a06f4ce2ae49a69a0105
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="secure-the-snapshot-folder"></a>保護快照集資料夾
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 快照集資料夾是儲存快照集檔案的目錄；建議您將此目錄專用於快照集儲存。 授與「快照集代理程式」對資料夾的寫入權限，並確定僅授與 Windows 帳戶讀取權限，「合併代理程式」或「散發代理程式」使用該帳戶來存取此資料夾。 與代理程式相關聯的 Windows 帳戶必須為網域帳戶，這樣才能存取位於遠端電腦上的快照集資料夾。  
  
> [!NOTE]  
>  使用者帳戶控制 (UAC) 可協助管理員管理其較高的使用者權限 (有時也稱為「權限」) 。 在已啟用 UAC 的作業系統上執行時，管理員不會使用其管理權限。 反而會以標準 (非管理員) 使用者的身分執行大部分的動作，只有在必要時才會採用其管理權限。 UAC 可以防止以管理員權限存取快照共用。 因此，您必須針對快照集代理程式、散發代理程式和合併代理程式所使用的 Windows 帳戶，明確地授與快照集共用權限。 即使 Windows 帳戶是管理員群組的成員，也必須這麼做。  
  
 透過 [設定散發精靈] 或 [新增發行集精靈] 設定「散發者」時，快照集資料夾預設為本機路徑：X:\Program Files\Microsoft SQL Server\\*\<執行個體>*\MSSQL\ReplData。 如果您使用的是遠端「散發者」或提取訂閱，則必須指定 UNC 網路共用 (例如 \\\\<*電腦名稱>*\snapshot) 而不是本機路徑。  
  
 授與快照集資料夾存取權限時，您必須依據存取資料夾的方式授與它們權限。 下列對話方塊索引標籤用於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2003：  
  
-   如果您指定的是本機路徑，則可透過 **[屬性]** 對話方塊的 **[安全性]** 索引標籤授與對該資料夾的存取權限。  
  
-   如果您指定的是網路共用，則可透過 **[屬性]** 對話方塊的 **[共用]** 索引標籤授與對該資料夾的存取權限。  
  
    > [!NOTE]  
    >  如果複寫代理程式在「散發者」上執行，請使用 **[屬性]** 對話方塊的 **[安全性]** 索引標籤，此資料夾才能授與權限給用來執行此代理程式的 Windows 帳戶。 即使在使用網路共用時，也要進行這項處理。 當「發行者」和「散發者」位於相同電腦上時，這會套用到發送訂閱的「合併代理程式」和「散發代理程式」及套用到「快照集代理程式」。  
  
 如需設定本機路徑和網路共用權限的詳細資訊，請參閱 Windows 文件集。  
  
> [!NOTE]  
>  如果卸除發行集，則複寫會嘗試移除 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶之安全性內容下的快照集資料夾。 如果此帳戶沒有足夠的權限，則使用具有足夠權限的帳戶登入並手動移除該資料夾。 如果資料夾是本機路徑，移除資料夾需要有 **修改** 權限，如果資料夾是網路路徑，則需要有 **完全控制** 權限。  
  
## <a name="delivering-snapshots-through-ftp"></a>透過 FTP 傳遞快照集  
 建議安全性最佳做法是將快照集儲存在 UNC 共用中，但是快照集也可以先儲存在 FTP 共用中，然後再透過 FTP 傳遞到「訂閱者」。 設定 FTP 伺服器時，請確定虛擬目錄公開基礎 UNC 共用，該共用允許發行集之「快照集代理程式」的寫入存取權限。  
  
 若要設定「訂閱者」為透過 FTP 擷取「快照集」，首先要設定具有 FTP 登入與密碼的 FTP 伺服器 (允許「訂閱者」有讀取 (或「取得」) 存取權限)，以允許其下載快照集檔案。  
  
 若要透過 FTP 傳遞快照集，請參閱[透過 FTP 傳遞快照集](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)。  
  
 如需有關設定和變更透過 FTP 存取快照集之密碼的詳細資訊，請參閱＜ [Secure the Publisher](../../../relational-databases/replication/security/secure-the-publisher.md)＞主題中的＜FTP 快照集傳遞＞一節。  
  
## <a name="see-also"></a>另請參閱  
 [替代快照集資料夾位置](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [使用快照集初始化訂閱](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全性與保護 &#40;複寫&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [透過 FTP 傳送快照集](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)  
  
  
