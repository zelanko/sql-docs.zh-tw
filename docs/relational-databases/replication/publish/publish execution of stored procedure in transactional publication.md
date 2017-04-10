---
title: "在交易式發行集中發行預存程序的執行項 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "發行 [SQL Server 複寫], 預存程序執行"
  - "預存程序 [SQL Server 複寫], 發行"
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 在交易式發行集中發行預存程序的執行項 (SQL Server Management Studio)
  指定執行預存程序 （而非只是其定義），應該在發行 **發行項屬性-\< 發行項>** 對話方塊。 此對話方塊，請在新增發行集精靈和 **發行集屬性-\< 發行集>** 對話方塊。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
 初始化訂閱時，會將程序的定義 (CREATE PROCEDURE 陳述式) 複寫到訂閱者；在發行者端執行程序時，複寫會在訂閱者端執行對應的程序。  
  
### 若要發行預存程序的執行  
  
1.  在 **文章** 新增發行集精靈 」 頁面或 **發行集屬性-\< 發行集>** 對話方塊方塊中，選取預存程序。  
  
2.  按一下 **[發行項屬性]**，然後再按 **[設定反白顯示預存程序的屬性]**。  
  
3.  在 **發行項屬性-\< 發行項>** 對話方塊方塊中，指定下列值的其中一個 **複寫** 選項︰  
  
    -   **[預存程序的執行]**  
  
    -   **[SP 的序列式交易執行]**  
  
         這是建議選項，因為它只會在程序於可序列化的交易內執行時複寫程序執行。 如果預存程序在序列化交易外部執行，則對已發行資料表中所做的資料變更會複寫為一連串的資料管理語言 (DML) 陳述式。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
## 另請參閱  
 [在異動複寫中發行預存程序執行](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  