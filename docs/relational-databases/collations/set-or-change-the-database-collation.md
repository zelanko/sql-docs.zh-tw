---
description: 設定或變更資料庫定序
title: 設定或變更資料庫定序 | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7fbaf22758dcf62d2159e63ee3af3c0507f3f607
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460571"
---
# <a name="set-or-change-the-database-collation"></a>設定或變更資料庫定序
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  本主題說明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來設定及變更資料庫定序。 如果沒有指定定序，會使用伺服器定序。  
  
> [!IMPORTANT]
> Azure SQL Database 不支援 `ALTER DATABASE COLLATE` 陳述式。

 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目設定或變更資料庫定序：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   僅限 Windows Unicode 定序只能搭配 COLLATE 子句使用，以便將定序套用至資料行層級和運算式層級資料的 **nchar**、 **nvarchar** 和 **ntext** 資料類型。 這些定序無法搭配 COLLATE 子句使用，以變更資料庫或伺服器執行個體的定序。  
  
-   如果指定的定序或所參考物件所用的定序使用 Windows 不支援的字碼頁， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會顯示錯誤。  

###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
您可以在 [Windows 定序名稱 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) 和 [SQL Server 定序名稱 &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)中找到支援的定序名稱；您也可以使用 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) 系統函數。  
  
當您變更資料庫定序時，會變更下列各項：  
  
-   系統資料表中的任何 **char**、 **varchar**、 **text**、 **nchar**、 **nvarchar**，或 **ntext** 資料行都會變更為新定序。  
  
-   預存程序與使用者定義函數的所有現有 **char**、 **varchar**、 **text**、 **nchar**、 **nvarchar** 或 **ntext** 參數和純量傳回值，都會變更為新定序。  
  
-   **char**、 **varchar**、 **text**、 **nchar**、 **nvarchar** 或 **ntext** 系統資料類型，以及以這些系統資料類型為基礎的所有使用者定義資料類型，都會變更為新的預設定序。  
  
您可以使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式的 `COLLATE` 子句，變更在使用者資料庫中建立之任何新物件的定序。 此陳述式 **不會變更** 現有使用者定義資料表中的資料行定序。 您可以使用 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 的 `COLLATE` 子句進行變更。  

> [!IMPORTANT]
> 變更資料庫或個別資料行的定序 **無法修改** 已經儲存在現有資料表中的基礎資料。 除非您的應用程式會明確處理不同定序之間的資料轉換與比較，否則仍建議您將資料庫中的現有資料轉換為新定序。 這麼做就能夠移除應用程式可能錯誤地修改資料，而可能導致錯誤結果或靜態資料遺失的風險。   

變更資料庫定序時，根據預設，只有新的資料表會繼承新的資料庫定序。 您可以使用幾個替代方法，將現有資料轉換為新的定序：
-  就地轉換資料。 若要轉換現有資料表中資料行的定序，請參閱[設定或變更資料行定序](../../relational-databases/collations/set-or-change-the-column-collation.md)。 這種作業很容易實作，但對於大型資料表與忙碌的應用程式而言可能是造成阻礙的問題。 請參閱下列範例，了解如何將 `MyString` 資料行就地轉換為新的定序：

   ```sql
   ALTER TABLE dbo.MyTable
   ALTER COLUMN MyString VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8;
   ```

-  將資料複製到使用新定序的新資料表，並取代相同資料庫中的原始資料表。 在目前資料庫中建立新的資料表，該資料庫會繼承資料庫定序、複製舊資料表與新資料表的資料、捨棄原始資料表，並將新資料表重新命名為原始資料表的名稱。 這是比就地轉換更快速的作業，但在處理具有相依性的複雜結構描述 (例如外部索引鍵條件約束、主索引鍵條件約束與觸發程序) 時，則可能會難以執行。 若應用程式持續變更資料，則此作業在最後的截斷點前，還需要為原始資料表與新資料表之間的資料進行最後同步處理。 請參閱下列範例，了解如何將 `MyString` 資料行「複製並取代」轉換為新的定序：

   ```sql
   CREATE TABLE dbo.MyTable2 (MyString VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8); 
   
   INSERT INTO dbo.MyTable2 
   SELECT * FROM dbo.MyTable; 
   
   DROP TABLE dbo.MyTable; 
   
   EXEC sp_rename 'dbo.MyTable2', 'dbo.MyTable’;
   ```

-  將資料複製到使用新定序的新資料庫，並取代原始資料庫。 使用新定序建立新的資料庫，然後透過 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [匯入/匯出精靈] 等工具，從原始資料庫傳輸資料。 對於複雜的結構描述而言，這是較為簡單的方法。 若應用程式持續變更資料，則此作業在最後的截斷點前，還需要為原始資料庫與新資料庫之間的資料進行最後同步處理。
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 若要建立新資料庫，需要 **master** 資料庫中的 `CREATE DATABASE` 權限，或需要 `CREATE ANY DATABASE` 或 `ALTER ANY DATABASE` 權限。  
  
 若要變更現有資料庫的定序，需要資料庫的 `ALTER` 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-or-change-the-database-collation"></a>若要設定或變更資料庫定序  
  
1.  在 [物件總管]  中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，展開該執行個體，然後展開 [資料庫]  。  
  
2.  如果您要建立新資料庫，以滑鼠右鍵按一下 **[資料庫]** ，然後按一下 **[新增資料庫]** 。 如果不要預設定序，請按一下 **[選項]** 頁面，然後從 **[定序]** 下拉式清單中選取定序。  
  
     或者，如果資料庫已經存在，以滑鼠右鍵按一下所要的資料庫，然後按一下 **[屬性]** 。 按一下 **[選項]** 頁面，然後從 **[定序]** 下拉式清單中選取定序。  
  
3.  完成後，請按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-set-the-database-collation"></a>若要設定資料庫定序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [COLLATE](~/t-sql/statements/collations.md) 子句來指定定序名稱。 範例會建立使用 `MyOptionsTest` 定序的 `Latin1_General_100_CS_AS_SC` 資料庫。 在您建立資料庫之後，執行 `SELECT` 陳述式以驗證設定。  
  
```sql  
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
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何在 [ALTER DATABASE](~/t-sql/statements/collations.md) 陳述式中使用 [COLLATE](../../t-sql/statements/alter-database-transact-sql.md) 子句，以變更定序名稱。 執行 `SELECT` 陳述式以驗證變更。  
  
```sql  
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
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
