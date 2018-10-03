---
title: 快照集代理程式 (新增發行集精靈) | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.configuresnapshotagent.f1
ms.assetid: 0257d4ee-1f7b-49fd-b4ef-65bfc1ef6951
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ede30c7586e3a613a5ce96dee8d824e2d88e14fe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48109108"
---
# <a name="snapshot-agent-new-publication-wizard"></a>快照集代理程式 (新增發行集精靈)
  快照集代理程式會建立檔案，檔案中包含用來初始化新訂閱的發行集結構描述和資料。 依預設，在新增發行集精靈中建立發行集之後，會立即執行快照集代理程式。 此後，代理程式就根據您指定的排程來執行。 代理程式每次執行時是否建立新的快照集檔案，視選擇的複寫類型和選項而定。 如需詳細資訊，請參閱[建立和套用快照集](create-and-apply-the-snapshot.md)。  
  
 對於使用參數化篩選的合併式發行集，在完成發行集快照集之後，您必須為資料的每一個資料分割建立快照集。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
## <a name="options"></a>選項。  
 **[立即建立快照集]** (合併式複寫) 或 **[立即建立快照集，並保留快照集為可使用狀態，以初始化訂閱]** (異動複寫)  
 選取此核取方塊即可在完成新增發行集精靈之後立即建立快照集。 如果您想要在產生快照集之後變更 **[發行集屬性]** 對話方塊中的快照集屬性，或要初始化不具有快照集的訂閱者，請清除此核取方塊。 如需詳細資訊，請參閱 [不使用快照集初始化交易式訂閱](initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
> [!NOTE]  
>  精靈可能會提示散發者的連接，以便為散發者代理程式或合併代理程式啟動適當的作業。  
  
 **排程快照集代理程式在下列時間執行**  
 接受執行快照集代理程式的預設排程，或按一下 **[變更]** 來指定排程。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](publish/create-a-publication.md)   
 [建立和套用初始快照集](create-and-apply-the-initial-snapshot.md)   
 [檢視及修改發行集屬性](publish/view-and-modify-publication-properties.md)   
 [使用快照集初始化訂閱](initialize-a-subscription-with-a-snapshot.md)   
 [發行資料和資料庫物件](publish/publish-data-and-database-objects.md)   
 [複寫代理程式概觀](agents/replication-agents-overview.md)  
  
  
