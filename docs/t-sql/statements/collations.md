---
title: "定序 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLLATE
- COLLATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], COLLATE clause
- COLLATE clause
ms.assetid: 76763ac8-3e0d-4bbb-aa53-f5e7da021daa
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7a206f638b78a5e4311ab7889a7902aa39a17413
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="collations"></a>定序
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  這是可套用至資料庫定義或資料行定義來定義定序，或套用至字元字串運算式來套用定序轉換的子句。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
COLLATE { <collation_name> | database_default }  
<collation_name> :: =   
     { Windows_collation_name } | { SQL_collation_name }  
```  
  
## <a name="arguments"></a>引數  
 *collation_name*  
 套用至運算式、資料行定義或資料庫定義之定序的名稱。 *sys.databases*可以只指定*Windows_collation_name*或*SQL_collation_name*。 *sys.databases*必須是常值。 *sys.databases*無法由變數或運算式。  
  
 *Windows_collation_name*的定序名稱[Windows 定序名稱](../../t-sql/statements/windows-collation-name-transact-sql.md)。  
  
 *SQL_collation_name*的定序名稱[SQL Server 定序名稱](../../t-sql/statements/sql-server-collation-name-transact-sql.md)。  
  
 在資料庫定義層級套用定序時，僅限 Unicode 的 Windows 定序就無法搭配 COLLATE 子句使用。  
  
 **database_default**  
 使 COLLATE 子句繼承目前資料庫的定序。  
  
## <a name="remarks"></a>備註  
 您可以在許多層級指定 COLLATE 子句。 這些選項包括：  
  
1.  建立或變更資料庫。  
  
     您可以利用 CREATE DATABASE 或 ALTER DATABASE 陳述式的 COLLATE 子句來指定資料庫的預設定序。 您也可以在利用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來建立資料庫時指定定序。 如果您沒有指定定序，就會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的預設定序指派給資料庫。  
  
    > [!NOTE]  
    >  Windows 僅限 Unicode 定序只能搭配 COLLATE 子句來套用定序來**nchar**， **nvarchar**，和**ntext**資料行層級上的資料類型和運算式層級資料;它們不能搭配 COLLATE 子句以變更資料庫或伺服器執行個體的定序。  
  
2.  建立或變更資料表資料行。  
  
     您可以利用 CREATE TABLE 或 ALTER TABLE 陳述式的 COLLATE 子句來指定每個字元字串資料行的定序。 您也可以在利用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來建立資料表時指定定序。 如果您沒有指定定序，就會將資料庫的預設定序指派給資料行。  
  
     您也可以使用`database_default`COLLATE 子句中指定暫存資料表中的資料行使用目前的使用者資料庫預設定，而不是連接的選項**tempdb**。  
  
3.  轉換運算式的定序。  
  
     您可以利用 COLLATE 子句，將字元運算式套用至特定定序。 字元常值和變數會被指派目前資料庫的預設定序。 資料行參考會被指派資料行的定義定序。  
  
 識別碼的定序會隨定義的層級而不同。 執行個體層級物件 (如登入和資料庫名稱) 的識別碼會被指派執行個體的預設定序。 資料庫內之物件 (如資料表、檢視和資料行名稱) 的識別碼會被指派資料庫的預設定序。 例如，兩份大小寫不同的同名資料表，可以建立在定序區分大小寫的資料庫中，但不能建立在定序不區分大小寫的資料庫中。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
 當連接內容只有一個相關聯資料庫時，可以建立變數、GOTO 標籤、暫時預存程序和暫存資料表，之後當內容切換到另一個資料庫時，可以參考它們。 變數、GOTO 標籤、暫存預存程序和暫存資料表的識別碼都位於伺服器執行個體的預設定序中。  
  
 COLLATE 子句使用，可套用至只有**char**， **varchar**，**文字**， **nchar**， **nvarchar**與**ntext**資料型別。  
  
 COLLATE 會使用*collate_name*以參考 SQL Server 定序或 Windows 定序套用至運算式、 資料行定義或資料庫定義的名稱。 *sys.databases*可以只指定*Windows_collation_name*或*SQL_collation_name*而且此參數必須包含常值。 *sys.databases*無法由變數或運算式。  
  
 定序通常是用定序名稱來識別，但在安裝程式中除外。 在安裝程式，您可以改為指定 Windows 定序時，根定序指示項 （定序地區設定），然後指定 區分或不區分大小寫或腔調字的排序選項。  
  
 您可以執行系統函數[fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)擷取 Windows 定序和 SQL Server 定序的所有有效定序名稱的清單：  
  
```sql  
SELECT name, description  
FROM fn_helpcollations();  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只能支援基礎作業系統所支援的字碼頁。 當您執行視定序而定的動作時，所參考的物件使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序必須使用電腦上執行的作業系統所支援的字碼頁。 這些動作包括：  
  
-   當您建立或變更資料庫時，指定資料庫的預設定序。  
  
-   當您建立或變更資料表時，指定資料行的定序。  
  
-   當還原或附加資料庫、 資料庫的預設定序和任何定序**char**， **varchar**，和**文字**資料行或在資料庫中的參數必須支援的作業系統。  
  
> [!NOTE]
> 字碼頁翻譯支援**char**和**varchar**資料類型，但不適用於**文字**資料型別。 不會報告字碼頁轉換期間所遺失的資料。  
  
> [!NOTE]
> 如果指定的定序或所參考物件使用的定序使用 Windows，不支援的字碼頁[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會顯示錯誤。  
  
## <a name="examples"></a>範例  
  
### <a name="a-specifying-collation-during-a-select"></a>A. 在選取時指定定序  
 下列範例會建立簡單的資料表並且插入 4 個資料列。 然後範例會在從資料表選取資料時套用兩個定序，並且示範如何以不同的方式排序 `Chiapas`。  
  
```sql  
CREATE TABLE Locations  
(Place varchar(15) NOT NULL);  
GO  
INSERT Locations(Place) VALUES ('Chiapas'),('Colima')  
                             , ('Cinco Rios'), ('California');  
GO  
--Apply an typical collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Latin1_General_CS_AS_KS_WS ASC;  
GO  
-- Apply a Spanish collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Traditional_Spanish_ci_ai ASC;  
GO  
```  

以下是第一個查詢的結果。  
  
```
Place 
------------- 
California 
Chiapas 
Cinco Rios 
Colima
```  
  
以下是第二個查詢的結果。  
 
```
Place 
------------- 
California 
Cinco Rios 
Colima 
Chiapas
```  
  
### <a name="b-additional-examples"></a>B. 其他範例  
 如需使用的其他範例**COLLATE**，請參閱[CREATE DATABASE &#40;SQL Server TRANSACT-SQL &#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md#examples)範例**G.建立資料庫並指定定序名稱和選項**，和[ALTER TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md#alter_column)範例**V.變更資料行定序**。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)    
 [定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)    
 [定序優先順序 &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)     
 [常數 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)     
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)     
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)     
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)     
 [資料表 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/table-transact-sql.md)     
  
  
