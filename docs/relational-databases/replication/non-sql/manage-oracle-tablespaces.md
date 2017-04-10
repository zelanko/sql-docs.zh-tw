---
title: "管理 Oracle 資料表空間 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Oracle 發行 [SQL Server 複寫], 管理資料表空間"
  - "資料表空間 [SQL Server 複寫]"
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 管理 Oracle 資料表空間
  資料表空間是資料庫的儲存單位，大致相當於中的檔案群組 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 資料表空間允許在個別群組中儲存和管理資料庫物件。 如需詳細資訊，請參閱 Oracle 文件集。  
  
 將資料表設定為 Oracle 發行集的一部分，您可以在儲存複寫記錄資訊時選擇性地指定使用現有的 Oracle 資料表空間。 如果未指定，則複寫物件的資料表空間為與複寫管理使用者結構描述相關的預設資料表空間，該複寫管理使用者結構描述在設定「發行者」時設定。  
  
 **若要指定發行項記錄資料表的資料表空間**:  
  
-   指定在資料表空間 **發行項屬性** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
-   使用 [sp_changearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)。 若要使用 **sp_changearticle**, ，指定下列各項︰  
  
    -   Oracle 發行者 」 的參數名稱 **@publisher**。  
  
    -   參數的 Oracle 發行集名稱 **@publication**。  
  
    -   參數的發行項名稱 **@article**。  
  
    -   資料表空間' 參數值 **@property**。  
  
    -   參數的表格區名稱 **@value**。  
  
## 另請參閱  
 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [在 Oracle 發行者端建立的物件](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)  
  
  