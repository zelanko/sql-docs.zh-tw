---
title: "設定或變更資料庫定序 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: collations
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7c787c1399715b4e0a3bff74a4f4e8f6c802816c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="set-or-change-the-database-collation"></a>設定或變更資料庫定序
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定及變更資料庫定序。 如果沒有指定定序，會使用伺服器定序。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目設定或變更資料庫定序：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   僅限 Windows Unicode 定序只能搭配 COLLATE 子句使用，以便將定序套用至資料行層級和運算式層級資料的 **nchar**、 **nvarchar**和 **ntext** 資料類型。 這些定序無法搭配 COLLATE 子句使用，以變更資料庫或伺服器執行個體的定序。  
  
-   如果指定的定序或所參考物件所用的定序使用 Windows 不支援的字碼頁， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會顯示錯誤。  
  
###  <a name="Recommendations"></a> 建議  
  
-   您可以在 [Windows 定序名稱 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) 和 [SQL Server 定序名稱 &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)中找到支援的定序名稱；您也可以使用 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) 系統函數。  
  
-   當您變更資料庫定序時，會變更下列各項：  
  
    -   系統資料表中的任何 **char**、 **varchar**、 **text**、 **nchar**、 **nvarchar**，或 **ntext** 資料行都會變更為新定序。  
  
    -   預存程序與使用者定義函數的所有現有 **char**、 **varchar**、 **text**、 **nchar**、 **nvarchar**或 **ntext** 參數和純量傳回值，都會變更為新定序。  
  
    -   **char**、 **varchar**、 **text**、 **nchar**、 **nvarchar**或 **ntext** 系統資料類型，以及以這些系統資料類型為基礎的所有使用者定義資料類型，都會變更為新的預設定序。  
  
-   您可以使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式的 COLLATE 子句，變更在使用者資料庫中建立的任何新物件的定序。 此陳述式不會變更現有使用者自訂資料表中的資料行定序。 您可以使用 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)的 COLLATE 子句進行變更。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 CREATE DATABASE  
 需要 **master** 資料庫的 CREATE DATABASE 權限，或需要 CREATE ANY DATABASE 或 ALTER ANY DATABASE 權限。  
  
 ALTER DATABASE  
 需要資料庫的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-or-change-the-database-collation"></a>若要設定或變更資料庫定序  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，展開該執行個體，然後展開 [資料庫] 。  
  
2.  如果您要建立新資料庫，以滑鼠右鍵按一下 **[資料庫]** ，然後按一下 **[新增資料庫]**。 如果不要預設定序，請按一下 **[選項]** 頁面，然後從 **[定序]** 下拉式清單中選取定序。  
  
     或者，如果資料庫已經存在，以滑鼠右鍵按一下所要的資料庫，然後按一下 **[屬性]**。 按一下 **[選項]** 頁面，然後從 **[定序]** 下拉式清單中選取定序。  
  
3.  完成後，請按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-set-the-database-collation"></a>若要設定資料庫定序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例示範如何使用 [COLLATE](~/t-sql/statements/collations.md) 子句來指定定序名稱。 範例會建立使用 `MyOptionsTest` 定序的 `Latin1_General_100_CS_AS_SC` 資料庫。 在您建立資料庫之後，執行 `SELECT` 陳述式以驗證設定。  
  
```tsql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE Latin1_General_100_CS_AS_SC;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
#### <a name="to-change-the-database-collation"></a>若要變更資料庫定序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例示範如何在 [ALTER DATABASE](~/t-sql/statements/collations.md) 陳述式中使用 [COLLATE](../../t-sql/statements/alter-database-transact-sql.md) 子句，以變更定序名稱。 執行 `SELECT` 陳述式以驗證變更。  
  
```tsql  
USE master;  
GO  
ALTER DATABASE MyOptionsTest  
COLLATE French_CI_AS ;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [SQL Server 定序名稱 &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)   
 [Windows 定序名稱 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)   
 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [定序優先順序 &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
