---
title: "在散發者端啟用遠端發行者 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "遠端散發者 [SQL Server 複寫]"
  - "發行者 [SQL Server 複寫]"
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# 在散發者端啟用遠端發行者 (SQL Server Management Studio)
  啟用 「 發行者 」 上使用遠端散發者 **發行者** 頁面。 此頁面可用於設定散發精靈和 **散發者屬性-\< 散發者>** 對話方塊。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [設定發行與散發](../../relational-databases/replication/configure-publishing-and-distribution.md) 和 [檢視和修改 「 散發者 」 和 「 發行者 」 屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
### 若要在設定散發精靈中啟用發行者  
  
1.  在 **發行者** 頁面的 「 設定散發精靈 」 中，按一下 [ **新增**。  
  
2.  按一下 [ **加入 SQL Server 發行者**。 啟用 Oracle 發行者使用散發者的相關資訊，請參閱 [從 Oracle 資料庫建立發行集](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)。  
  
3.  在 **連接到伺服器** 對話方塊方塊中，指定連接資訊的 「 發行者 」 使用遠端散發者，然後按一下 [ **連接**。  
  
4.  在 **散發者密碼** 頁面上，於 **密碼** 和 **確認密碼** 文字方塊中，指定強式密碼 **distributor_admin** 帳戶，複寫將用來從 「 發行者 」 連接到散發者執行管理工作。  
  
5.  若要檢視和修改發行者的設定，請按一下屬性按鈕 (**...**)。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### 若要在散發者屬性對話方塊中啟用發行者  
  
1.  在 **發行者** 頁面 **散發者屬性-\< 散發者>** 對話方塊中，按一下 [ **新增**。  
  
2.  按一下 [ **加入 SQL Server 發行者**。 啟用 Oracle 發行者使用散發者的相關資訊，請參閱 [從 Oracle 資料庫建立發行集](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)。  
  
3.  在 **連接到伺服器** 對話方塊方塊中，指定連接資訊的 「 發行者 」 使用遠端散發者，然後按一下 [ **連接**。  
  
4.  在 **發行者** 頁面上，於 **密碼** 和 **確認密碼** 文字方塊中，指定強式密碼 **distributor_admin** 帳戶，複寫將用來從 「 發行者 」 連接到散發者執行管理工作。  
  
5.  若要檢視和修改發行者的設定，請按一下屬性按鈕 (**...**)。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 另請參閱  
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [設定散發](../../relational-databases/replication/configure-distribution.md)   
 [保護散發者](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  