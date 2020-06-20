---
title: 新的對等 (Peer) 初始化 (點對點複寫) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.init.f1
ms.assetid: 050c00e1-78bd-4d9c-affe-40e22feb4d94
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ef3f20d6757b056abe925e087e81e07ad6358696
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060661"
---
# <a name="new-peer-initialization-peer-to-peer-replication"></a>新的對等 (Peer) 初始化 (點對點複寫)
  您可以使用 **[新的對等 (Peer) 初始化]** 頁面來指定對等 (Peer) 資料庫的初始化方式 （必須先初始化對等，才能完成此嚮導）。對等會以手動方式初始化，或使用由異動複寫所提供的「**使用初始化」和「備份**」功能。 （點對點異動複寫不支援使用快照集初始化對等）。如果必須使用不同的方法來初始化不同的對等，您必須執行嚮導多次來個別新增對等。  
  
## <a name="options"></a>選項  
 **指定要如何初始化新的對等 (Peer) 資料庫**  
 所有發行物件的結構描述和資料，都必須存在於每一個對等 (Peer) 上。 選取下列其中一個選項：  
  
-   如果您已手動建立發行物件的結構描述，或者已還原備份，而且第一個發行集資料庫在建立備份之後未變更任何資料，請選取第一個選項。 如果您是手動建立結構描述，就必須確定所有必要的資料存在於每一個對等 (Peer) 上。 此選項對應至訂閱屬性 **sync_type** 的 **replication support only**值。  
  
-   如果您已還原備份，且第一個發行集資料庫在執行備份之後已變更資料，請選取第二個選項。 如此一來，複寫就必須傳遞來自第一個發行集資料庫中、未包含在備份內的變更。 此選項對應至訂閱屬性 **sync_type** 的 **initialize with backup**值。  
  
     發行集啟用點對點複寫時，會設定 **allow_initialize_from_backup** 發行集屬性。 複寫會立即開始追蹤第一個發行集資料庫的變更。 因此，在已選取 **initialize with backup** 選項的情況下，這些變更就可以傳遞至一或多個對等 (Peer) 的還原資料庫。 按一下 **[瀏覽]** 按鈕找出所使用的備份，而且複寫將從備份中讀取記錄序號 (LSN)。 在第一個發行集資料庫中，具有較高 LSN 的所有變更將會傳遞至每一個對等 (Peer)。  
  
     如果您正在建立或加入至包含 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的拓撲，這個選項可能無法使用。 下表顯示了當您將節點加入至現有拓撲時，這個選項是否可用。  
  
    |新節點|第一個節點|其他節點|選項|  
    |--------------|----------------|----------------------|------------|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|已停用|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|None|已停用|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|已停用|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|None|啟用|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|None|啟用|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|啟用|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|None|啟用|  
  
## <a name="see-also"></a>另請參閱  
 [管理點對點拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [@loopback_detection](transactional/peer-to-peer-transactional-replication.md)  
  
  
