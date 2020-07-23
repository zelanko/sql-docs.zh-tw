---
title: 新增與卸除發行項 (SSMS)
description: 描述如何使用 SQL Server Management Studio (SSMS) 在發行集中新增和卸除發行項。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- dropping articles
- adding articles
- articles [SQL Server replication], adding
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1a32aabcd7eb431498e54a828dcfdcf4e87480c1
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923684"
---
# <a name="add-articles-to-and-drop-articles-from-a-publication"></a>在發行集中新增和卸除發行項
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  當您在「新增發行集精靈」中建立發行集後，最開始要向其中新增發行項。 如需使用此精靈的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
 建立發行集之後，在 [發行集屬性 - \<Publication>] 對話方塊的 [發行項] 頁面中，新增和刪除發行項。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。 如需新增及卸除發行項的詳細資訊，請參閱[在現有發行集中新增和卸除發行項](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
### <a name="to-add-an-article-after-a-publication-is-created"></a>若要在建立發行集之後新增發行項  
  
1.  在 [發行集屬性 - \<Publication>] 對話方塊的 [發行項] 頁面中，清除 [僅顯示清單中已核取的物件] 核取方塊。 這將允許您查看發行集資料庫中的未發行物件。  
  
2.  選取您要新增之每一個發行項旁邊的核取方塊。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-an-article"></a>若要刪除發行項  
  
1.  在 [發行集屬性 - \<Publication>] 對話方塊的 [發行項] 頁面中，清除所要刪除每個發行項旁邊的核取方塊。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
