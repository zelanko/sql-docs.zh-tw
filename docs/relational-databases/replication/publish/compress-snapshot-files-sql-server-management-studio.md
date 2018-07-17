---
title: 壓縮快照集檔案 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], compressed
- snapshot replication [SQL Server], compressed snapshots
ms.assetid: 174ade3e-74a1-4e67-a6da-b874be3ff50f
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 095b98e25fadb767b2cbf47511292daddf68e663
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37351000"
---
# <a name="compress-snapshot-files-sql-server-management-studio"></a>壓縮快照集檔案 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 [發行集屬性 - \<發行集>] 對話方塊的 [快照集] 頁面上，指定要壓縮檔案。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
### <a name="to-compress-snapshot-files"></a>若要壓縮快照集檔案  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [快照集] 頁面上：  
  
    1.  選取 **[將檔案放在下列資料夾中]**，然後按一下 **[瀏覽]** 以瀏覽至目錄，或者輸入應儲存快照集檔案之目錄的路徑。  
  
        > [!NOTE]  
        >  快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 若是使用提取訂閱，則必須指定一個共用目錄作為通用命名慣例 (UNC) 路徑，例如 \\\computername\snapshot。 如需詳細資訊，請參閱[保護快照集資料夾](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
    2.  除非您需要將快照集檔案寫入兩個位置，否則請清除 **[將檔案放在預設資料夾]** 。  
  
        > [!NOTE]  
        >  如果選取這個核取方塊，則不會壓縮儲存在預設資料夾中的檔案。 壓縮的檔案只能儲存在上一個步驟中指定的其他位置。  
  
2.  選取 **[壓縮此資料夾中的快照集檔案]**。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [設定快照集屬性 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [壓縮的快照集](../../../relational-databases/replication/compressed-snapshots.md)   
 [使用快照集初始化訂閱](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
