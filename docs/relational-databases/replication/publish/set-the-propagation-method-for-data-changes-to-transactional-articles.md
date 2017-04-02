---
title: "設定對交易式發行項之資料變更的傳播方法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "異動複寫，傳播方法"
  - "傳播資料變更 [SQL Server 複寫]"
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 設定對交易式發行項之資料變更的傳播方法
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，針對 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中交易式發行項的資料變更設定傳播方法。  
  
 根據預設，異動複寫會針對各發行項使用一組預存程序將變更傳遞至「訂閱者」。 您也可以使用自訂程序取代這些程序。 如需詳細資訊，請參閱 [指定如何傳播變更的交易式發行項](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要針對交易式發行項的資料變更設定傳播方法，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   編輯複寫所產生的任何快照集檔案時必須特別小心。 您必須在自訂預存程序中測試並支援自訂邏輯。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 不提供自訂邏輯的支援。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 指定傳遞方法上 **屬性** ] 索引標籤 **發行項屬性-\< 發行項>** 對話方塊中，也就是在新增發行集精靈和 **發行集屬性-\< 發行集>** 對話方塊。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 指定傳遞方法  
  
1.  在 **文章** 新的發行集精靈] 頁面或 **發行集屬性-\< 發行集>** 對話方塊中，選取資料表，然後按一下 **發行項屬性**。  
  
2.  按一下 **[設定反白顯示資料表發行項的屬性]**。  
  
3.  在 **屬性** ] 索引標籤的 **發行項屬性-\< 發行項>** 對話方塊中，於 **陳述式傳遞** 區段中，指定每個作業使用的傳播方法 **INSERT 傳遞格式**, ，**UPDATE 傳遞格式**, ，和 **DELETE 傳遞格式** 功能表。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
#### 產生及使用自訂預存程序  
  
1.  在 **文章** 新的發行集精靈] 頁面或 **發行集屬性-\< 發行集>** 對話方塊中，選取資料表，然後按一下 **發行項屬性**。  
  
2.  按一下 **[設定反白顯示資料表發行項的屬性]**。  
  
     上 **屬性** ] 索引標籤的 **發行項屬性-\< 發行項>** 對話方塊中，於 **陳述式傳遞** 區段中，從適當的傳遞格式] 功能表中選取的呼叫語法 (**INSERT 傳遞格式**, ，**UPDATE 傳遞格式**, ，或 **DELETE 傳遞格式**)，然後輸入要使用中的程序名稱 **INSERT 預存程序**, ，**刪除預存程序**, ，或 **更新預存程序**。 如需 CALL 語法的詳細資訊，請參閱 「 預存程序的呼叫語法 」 一節中 [指定如何傳播變更的交易式發行項](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
5.  產生發行集的快照集時，其中會包含您在前一個步驟中指定的程序。 這些程序將使用您指定的 CALL 語法，但是會包含複寫使用的預設邏輯。  
  
     產生快照集之後，導覽至這個發行項所屬發行集的快照集資料夾，並尋找與該發行項同名的 **.sch** 檔。 使用「記事本」或其他文字編輯器開啟這個檔案，尋找插入、更新或刪除預存程序的 CREATE PROCEDURE 命令，然後編輯程序定義以便提供傳遞資料變更所需的任何自訂邏輯。 如果快照集是重新產生的，則必須重新建立自訂程序。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 異動複寫可讓您控制變更要如何從發行者傳播至訂閱者，而且在建立發行項時，可以透過程式設計方式設定此傳播方法，並在稍後使用複寫預存程序加以變更。  
  
> [!NOTE]  
>  您可以針對發生在發行之資料列上的每一種類型的 DML (資料操作語言) 作業 (插入、更新或刪除) 指定不同的傳播方法。  
  
 如需詳細資訊，請參閱 [指定如何傳播變更的交易式發行項](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
#### 建立使用 Transact-SQL 命令的發行項來傳播資料變更  
  
1.  在發行集資料庫的發行者，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定發行項所屬的發行集名稱 **@publication**, ，發行項的名稱 **@article**, 發行的資料庫物件、 **@source_object**, ，且值為 **SQL** 至少一個下列參數︰  
  
    -   **@ins_cmd** -控制的複寫 [插入](../../../t-sql/statements/insert-transact-sql.md) 命令。  
  
    -   **@upd_cmd** -控制的複寫 [更新](../../../t-sql/queries/update-transact-sql.md) 命令。  
  
    -   **@del_cmd** -控制的複寫 [刪除](../../../t-sql/statements/delete-transact-sql.md) 命令。  
  
    > [!NOTE]  
    >  當指定的值為 **SQL** 任何上述參數，該類型的命令將會複寫到訂閱者端視 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令。  
  
     如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
#### 建立不會傳播資料變更的發行項  
  
1.  在發行集資料庫的發行者，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定發行項所屬的發行集名稱 **@publication**, ，發行項的名稱 **@article**, 發行的資料庫物件、 **@source_object**, ，且值為 **NONE** 至少一個下列參數︰  
  
    -   **@ins_cmd** -控制的複寫 [插入](../../../t-sql/statements/insert-transact-sql.md) 命令。  
  
    -   **@upd_cmd** -控制的複寫 [更新](../../../t-sql/queries/update-transact-sql.md) 命令。  
  
    -   **@del_cmd** -控制的複寫 [刪除](../../../t-sql/statements/delete-transact-sql.md) 命令。  
  
    > [!NOTE]  
    >  當指定的值為 **NONE** 任何上述參數，該類型的命令不會複寫到訂閱者。  
  
     如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
#### 使用使用者修改的自訂預存程序建立發行項  
  
1.  在發行集資料庫的發行者，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定發行項所屬的發行集名稱 **@publication**, ，發行項的名稱 **@article**, 、 發行的資料庫物件 **@source_object**, ，值 **@schema_option** 包含值的位元遮罩 **0x02** （啟用自動產生自訂預存程序），以及至少一個下列參數︰  
  
    -   **@ins_cmd** -指定的值為 **CALL sp_MSins_*article_name***, ，其中 ***article_name*** 值指定 **@article**。  
  
    -   **@del_cmd** -指定的值為 **呼叫 sp_MSdel_*article_name*** 或 **XCALL sp_MSdel_*article_name***, ，其中 ***article_name*** 值指定 **@article**。  
  
    -   **@upd_cmd** -指定的值為 **SCALL sp_MSupd_*article_name***, ，**呼叫 sp_MSupd_*article_name***, ，**XCALL sp_MSupd_*article_name***, ，或 **MCALL sp_MSupd_*article_name***, ，其中 ***article_name*** 值指定 **@article**。  
  
    > [!NOTE]  
    >  您可以針對上述的每一個命令參數，為複寫產生的預存程序指定您自己的名稱。  
  
    > [!NOTE]  
    >  如需有關呼叫、 SCALL、 XCALL 和 MCALL 語法的詳細資訊，請參閱 [指定如何傳播變更的交易式發行項](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
     如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  產生快照集之後，導覽至這個發行項所屬發行集的快照集資料夾，並尋找與該發行項同名的 **.sch** 檔。 使用 Notepad.exe 開啟這個檔案，尋找插入、更新或刪除預存程序的 CREATE PROCEDURE 命令，然後編輯程序定義以便提供傳播資料變更所需的任何自訂邏輯。 如需詳細資訊，請參閱 [指定如何傳播變更的交易式發行項](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
#### 使用自訂預存程序中的自訂指令碼建立發行項，以傳播資料變更  
  
1.  在發行集資料庫的發行者，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定發行項所屬的發行集名稱 **@publication**, ，發行項的名稱 **@article**, 、 發行的資料庫物件 **@source_object**, ，值 **@schema_option** 包含值的位元遮罩 **0x02** （啟用自動產生自訂預存程序），以及至少一個下列參數︰  
  
    -   **@ins_cmd** -指定的值為 **CALL sp_MSins_*article_name***, ，其中 ***article_name*** 值指定 **@article**。  
  
    -   **@del_cmd** -指定的值為 **呼叫 sp_MSdel_*article_name*** 或 **XCALL sp_MSdel_*article_name***, ，其中 ***article_name*** 值指定 **@article**。  
  
    -   **@upd_cmd** -指定的值為 **SCALL sp_MSupd_*article_name***, ，**呼叫 sp_MSupd_*article_name***, ，**XCALL sp_MSupd_*article_name***, ，**MCALL sp_MSupd_*article_name***, ，其中 ***article_name*** 值指定 **@article**。  
  
    > [!NOTE]  
    >  您可以針對上述的每一個命令參數，為複寫產生的預存程序指定您自己的名稱。  
  
    > [!NOTE]  
    >  如需有關呼叫、 SCALL、 XCALL 和 MCALL 語法的詳細資訊，請參閱 [指定如何傳播變更的交易式發行項](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
     如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在發行集資料庫的發行者，使用 [ALTER PROCEDURE](../../../t-sql/statements/alter-procedure-transact-sql.md) 陳述式，以編輯 [sp_scriptpublicationcustomprocs](../../../relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql.md) ，使它傳回 [建立程序](../../../t-sql/statements/create-procedure-transact-sql.md) 插入、 更新和刪除自訂預存程序的指令碼。 如需詳細資訊，請參閱 [指定如何傳播變更的交易式發行項](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
#### 變更傳播現有發行項之變更的方法  
  
1.  在發行集資料庫的發行者，執行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)。 指定 **@publication**, ，**@article**, ，值為 **ins_cmd**, ，**upd_cmd**, ，或 **del_cmd** 的 **@property**, ，而且適當的傳播方法 **@value**。  
  
2.  針對要變更的每一個傳播方法重複步驟 1。  
  
## 另請參閱  
 [指定交易式發行項變更的傳播方式](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)   
 [建立、 修改及刪除發行集和文件 & #40。複寫 & #41;](../../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)  
  
  