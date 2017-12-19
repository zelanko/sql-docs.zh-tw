---
title: "重新命名使用者定義函式 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: udf
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c2695a5c-9cc5-4b18-8771-53027ca9a9af
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2df378096ea362fc560141c9fa9744b9dee3917b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="rename-user-defined-functions"></a>重新命名使用者定義函數
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)] 您可以透過使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，重新命名 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的使用者定義函式。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目重新命名使用者定義函數：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   函數名稱必須符合 [識別碼](../../relational-databases/databases/database-identifiers.md)的規則。  
  
-   重新命名使用者定義函數，不會變更 **sys.sql_modules** 目錄檢視 definition 資料行中對應的物件名稱。 因此，我們建議您不要重新命名這個物件類型。 相反地，請卸除預存程序，再利用它的新名稱來重新建立預存程序。  
  
-   變更使用者定義函數的名稱或定義後，若未更新物件來反映對此函數所做的變更，則可能導致依存物件執行失敗。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 若要卸除函數，需要函數所屬結構描述的 ALTER 權限，或函數的 CONTROL 權限。 若要重新建立函數，需要資料庫的 CREATE FUNCTION 權限，以及此函數建立所在之結構描述的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rename-user-defined-functions"></a>若要重新命名使用者定義函數  
  
1.  在 **[物件總管]**中，按一下資料庫旁邊的加號，此資料庫包含要重新命名的函數。  
  
2.  按一下 **[可程式性]** 資料夾旁的加號。  
  
3.  按一下包含要重新命名之函數的資料夾旁邊的加號：  
  
    -   資料表值函式  
  
    -   純量值函式  
  
    -   彙總函式  
  
4.  以滑鼠右鍵按一下您要重新命名的函數，然後選取 [重新命名]。  
  
5.  輸入函數的新名稱。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要重新命名使用者定義函數**  
  
 您無法使用 Transact-SQL 陳述式來執行這項工作。 若要使用 Transact-SQL 來重新命名使用者定義函數，您必須先刪除現有的函數，然後使用新的名稱來重新建立函數。 確定使用函數舊名稱的所有程式碼和應用程式現在都使用新名稱。  
  
 如需詳細資訊，請參閱 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md) 和 [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [檢視使用者定義函數](../../relational-databases/user-defined-functions/view-user-defined-functions.md)  
  
  
