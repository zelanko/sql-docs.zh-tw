---
title: 刪除資料表 (Database Engine) | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table deletions [SQL Server]
- deleting tables
- removing tables
- dropping tables
ms.assetid: ca6aa3e9-9885-44c3-bafc-aec441fd97ec
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3c9dc1c5650c98a925ff79a9bc78917a80d73656
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909902"
---
# <a name="delete-tables-database-engine"></a>刪除資料表 (Database Engine)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中刪除 (卸除) 資料庫中的資料表。  
  
> [!CAUTION]  
>  在刪除資料表之前請仔細考慮。 如果現有的查詢、檢視表、使用者定義函數、預存程序或程式參考此資料表，則刪除將使這些物件失效。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來刪除資料表：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   您無法卸除 FOREIGN KEY 條件約束所參考的資料表。 您必須先卸除參考 FOREIGN KEY 條件約束或參考資料表。 如果參考資料表和持有要卸除的主索引鍵之資料表在相同的 DROP TABLE 陳述式中，就必須先列出參考資料表。  
  
-   當卸除資料表時，資料表的規則或預設值會失去它們的繫結，資料表的任何相關條件約束或觸發程序也都會自動卸除。 如果重新建立資料表，您必須重新繫結適當的規則和預設值、重新建立任何觸發程序，以及加入所有必要的條件約束。  
  
-   如果卸除的資料表包含具有 FILESTREAM 屬性的 **varbinary (max)** 資料行，則儲存在檔案系統中的任何資料都不會遭到移除。  
  
-   DROP TABLE 和 CREATE TABLE 不得在相同批次的相同資料表上執行。 否則，系統可能會發生非預期的錯誤。  
  
-   對於參考已卸除之資料表的任何檢視表或預存程序，您必須明確刪除或修改它們，以便移除資料表的參考。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料表所屬結構描述的 ALTER 權限、資料表的 CONTROL 權限，或 **db_ddladmin** 固定資料庫角色成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-table-from-the-database"></a>若要從資料庫刪除資料表  
  
1.  在 [物件總管] 中選取要刪除的資料表。  
  
2.  在資料表上按一下滑鼠右鍵，再從快速鍵功能表中選擇 [刪除]  。  
  
3.  訊息方塊會提示您確認是否刪除。 按一下 **[是]** 。  

    > [!NOTE]  
    >  刪除資料表會自動移除它的所有關聯性。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-table-in-query-editor"></a>若要在查詢編輯器中刪除資料表  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    DROP TABLE dbo.PurchaseOrderDetail;  
  
    ```  
  
 如需詳細資訊，請參閱 [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)。  
  
  
