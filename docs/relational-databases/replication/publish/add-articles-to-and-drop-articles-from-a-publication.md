---
title: "從發行集中加入和卸除發行項 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "發行項 [SQL Server 複寫], 卸除"
  - "刪除發行項"
  - "卸除發行項"
  - "加入發行項"
  - "發行項 [SQL Server 複寫], 加入"
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 從發行集中加入和卸除發行項 (SQL Server Management Studio)
  當您在「新增發行集精靈」中建立發行集後，最開始要向其中新增發行項。 如需使用此精靈的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
 在建立發行集之後，新增與刪除文件 **文章** 頁面 **發行集屬性-\< 發行集>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。 如需新增和卸除發行項考量的資訊，請參閱 [新增和卸除現有的發行集的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
### 若要在建立發行集之後新增發行項  
  
1.  在 **文章** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，清除 **放映才檢查清單中的物件** 核取方塊。 這將允許您查看發行集資料庫中的未發行物件。  
  
2.  選取您要新增之每一個發行項旁邊的核取方塊。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### 若要刪除發行項  
  
1.  在 **文章** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，清除核取方塊，您想要刪除的每個發行項旁邊。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## 另請參閱  
 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  