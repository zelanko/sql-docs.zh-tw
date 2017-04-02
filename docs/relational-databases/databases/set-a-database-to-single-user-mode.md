---
title: "將資料庫設定為單一使用者模式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "單一使用者模式 [SQL Server], 資料庫選項"
ms.assetid: fb5254eb-b635-4b39-8361-136fd36f2b1f
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 將資料庫設定為單一使用者模式
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中將使用者定義資料庫設定為單一使用者模式。 單一使用者模式指定一次只可有一位使用者存取資料庫，且一般是用於維護動作。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [必要條件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **使用下列方法，將資料庫設定為單一使用者模式：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果其他使用者可在將資料庫設定為單一使用者模式時連接到資料庫，則會關閉他們與資料庫的連接，而不會發出警告。  
  
-   即使設定該選項的使用者登出，資料庫仍會保持為單一使用者模式。 此時其他使用者可以連接到這個資料庫，但只能有一位。  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   將資料庫設為 SINGLE_USER 之前，請先確定 AUTO_UPDATE_STATISTICS_ASYNC 選項是否設為 OFF。 此選項設為 ON 時，更新統計資料的背景執行緒會取得資料庫連接，而您就無法以單一使用者模式存取資料庫。 如需詳細資訊，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料庫的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 若要將資料庫設定為單一使用者模式  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下要變更的資料庫，然後按一下 [屬性]。  
  
3.  在 [資料庫屬性]  對話方塊中按一下 [選項]  頁面。  
  
4.  從 **[限制存取]** 選項中，選取 **[單一]**。  
  
5.  如果其他使用者已連接到資料庫，則會出現 **[開啟連接]** 訊息。 若要變更屬性並關閉其他所有連接，請按一下 **[是]**。  
  
 您也可使用這個程序，將資料庫設定為多個或限制存取。 如需限制存取選項的詳細資訊，請參閱[資料庫屬性 &#40;選項頁面&#41;](../../relational-databases/databases/database-properties-options-page.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 若要將資料庫設定為單一使用者模式  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 這個範例會將資料庫設成 `SINGLE_USER` 模式來取得獨佔存取。 之後，範例會將 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的狀態設成 `READ_ONLY` ，並將資料庫的存取權還給所有使用者。終止選項 `WITH ROLLBACK IMMEDIATE` 是在第一個 `ALTER DATABASE` 陳述式中指定。 這會導致所有未完成的交易都會回復，而且 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的任何其他連接都會立即中斷。  
  
 [!code-sql[DatabaseDDL#AlterDatabase8](../../relational-databases/databases/codesnippet/tsql/set-a-database-to-single_1.sql)]  
  
## 另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  