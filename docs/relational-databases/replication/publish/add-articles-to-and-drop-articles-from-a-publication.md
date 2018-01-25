---
title: "在發行集中新增和卸除發行項 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- dropping articles
- adding articles
- articles [SQL Server replication], adding
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
caps.latest.revision: "35"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0dd2bf4ce4685125def4c87e0fc33fe974f49817
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="add-articles-to-and-drop-articles-from-a-publication"></a>在發行集中新增和卸除發行項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 當您在 [新增發行集精靈] 中建立發行集時，一開始要將發行項新增至發行集。 如需使用此精靈的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
 建立發行集之後，在 [發行集屬性 - \<發行集>] 對話方塊的 [發行項] 頁面中，新增和刪除發行項。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。 如需新增及卸除發行項的詳細資訊，請參閱[在現有發行集中新增和卸除發行項](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
### <a name="to-add-an-article-after-a-publication-is-created"></a>若要在建立發行集之後新增發行項  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [發行項] 頁面中，清除 [僅顯示清單中已核取的物件] 核取方塊。 這將允許您查看發行集資料庫中的未發行物件。  
  
2.  選取您要新增之每一個發行項旁邊的核取方塊。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-an-article"></a>若要刪除發行項  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [發行項] 頁面中，清除您要刪除之每個發行項旁邊的核取方塊。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
