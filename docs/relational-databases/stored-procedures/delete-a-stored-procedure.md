---
title: "刪除預存程序 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing stored procedures
- stored procedures [SQL Server], deleting
- deleting stored procedures
ms.assetid: 232dbf4d-392a-406f-af3a-579518cd8e46
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d9f9d65d2521299d34188897fbbf5675b5c9eea4
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="delete-a-stored-procedure"></a>刪除預存程序
    
##  <a name="Top"></a> 本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來刪除 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的預存程序。  
  
-   **開始之前：**[限制事項](#Restrictions)、[安全性](#Security)  
  
-   **使用下列項目刪除程序：**[SQL Server Management Studio](#SSMSProcedure)、[Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 刪除程序後，若未更新物件和指令碼來反映程序移除，則可能導致相依物件和指令碼執行失敗。 不過，如果所建立的相同名稱及相同參數的新程序是用以取代刪除的程序，其他參考該程序的物件仍然會成功地處理。 如需詳細資訊，請參閱 [檢視預存程序的相依性](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要程序所屬結構描述的 ALTER 權限，或程序的 CONTROL 權限。  
  
##  <a name="Procedures"></a> 如何刪除預存程序  
 您可以使用下列其中一項：  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要在物件總管中刪除程序**  
  
1.  在物件總管中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  依序展開 **[資料庫]**、程序所屬的資料庫，以及 **[可程式性]**。  
  
3.  展開 [預存程序]，以滑鼠右鍵按一下要移除的程序，然後按一下 [刪除]。  
  
4.  若要檢視相依於程序的物件，請按一下 **[顯示相依性]**。  
  
5.  確認已選取正確的程序，再按一下 **[確定]**。  
  
6.  從任何相依物件和指令碼中移除程序的參考。  
  
###  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要在查詢編輯器中刪除程序**  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  依序展開 **[資料庫]**、程序所屬的資料庫，或從工具列的可用資料庫清單中選取資料庫。  
  
3.  按一下 [檔案] 功能表上的 **[新增查詢]**。  
  
4.  取得要從目前資料庫移除之預存程序的名稱。 在 [物件總管] 中，依序展開 **[可程式性]** 與 **[預存程序]**。 或在查詢編輯器中，執行下列陳述式。  
  
    ```tsql  
    SELECT name AS procedure_name   
        ,SCHEMA_NAME(schema_id) AS schema_name  
        ,type_desc  
        ,create_date  
        ,modify_date  
    FROM sys.procedures;  
    ```  
  
5.  將下列範例複製並貼到查詢編輯器中，然後插入要從目前資料庫中刪除的預存程序名稱。  
  
    ```tsql  
    DROP PROCEDURE <stored procedure name>;  
    GO  
    ```  
  
6.  從任何相依物件和指令碼中移除程序的參考。  
  
## <a name="see-also"></a>另請參閱  
 [建立預存程序](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [修改預存程序](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [重新命名預存程序](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [檢視預存程序的定義](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [檢視預存程序的相依性](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
  
