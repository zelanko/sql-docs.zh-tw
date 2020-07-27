---
title: IDENTITY (屬性) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY property
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY property
- autonumbers, identity numbers
ms.assetid: 8429134f-c821-4033-a07c-f782a48d501c
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 48b8dbac5a4ad484103dcceedb243a52cc7e621d
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86943090"
---
# <a name="create-table-transact-sql-identity-property"></a>CREATE TABLE (Transact-SQL) IDENTITY (屬性)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  建立資料表中的識別欄位。 這個屬性會搭配 CREATE TABLE 和 ALTER TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式使用。  
  
> [!NOTE]  
>  IDENTITY 屬性不同於 SQL-DMO **Identity** 屬性，後者會公開資料行的資料列識別屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
IDENTITY [ (seed , increment) ]
```  
  
## <a name="arguments"></a>引數  
 *seed*  
 這是載入資料表的第一個資料列所用的值。  
  
 *increment*  
 這是加入先前載入的資料列之識別值的累加值。

 > [!NOTE]
 > 在 Azure Synapse Analytics 中，由於資料倉儲的分散式架構，識別值不會累加。 如需詳細資訊，請參閱[使用 IDENTITY 在 Synapse SQL 集區中建立 Surrogate 索引鍵](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-identity#allocation-of-values)。
  
 您必須同時指定種子和遞增，或同時不指定這兩者。 如果同時不指定這兩者，預設值便是 (1,1)。  
  
## <a name="remarks"></a>備註  
 識別欄位可用於產生索引鍵值。 資料行上的識別屬性可確保以下事項：  
  
-   根據目前種子與增量產生每個新值。  
  
-   特定交易的每個新值都與資料表上的其他並行交易不同。  
  
 資料行上的識別屬性不保證以下事項：  
  
-   **值的唯一性** - 必須使用 **PRIMARY KEY** 或 **UNIQUE** 條件約束或 **UNIQUE** 索引來強制執行唯一性。 - 
 
> [!NOTE]
> Azure Synapse Analytics 不支援 **PRIMARY KEY**、**UNIQUE** 條件約束或 **UNIQUE** 索引。 如需詳細資訊，請參閱[使用 IDENTITY 在 Synapse SQL 集區中建立 Surrogate 索引鍵](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-identity#what-is-a-surrogate-key)。

-   **交易內的連續值** - 插入多個資料列的交易並不保證能夠取得資料列的連續值，因為其他並行插入可能會在資料表中發生。 如果值必須是連續的，則交易應該使用資料表的獨佔鎖定，或使用 **SERIALIZABLE** 隔離等級。  
  
-   **重新啟動伺服器或其他失敗之後的連續值** -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會基於效能考量而快取識別值，因此在資料庫失敗或伺服器重新啟動期間，某些指派的值可能會遺失。 這可能會導致插入識別值之後的間隙。 若不接受間隙，則應用程式應會使用其擁有的機制，產生索引鍵值。 搭配使用順序產生器和 **NOCACHE** 選項時，可將間隙限制為從未認可的交易。  
  
-   **重複使用值** - 如果是具有特定種子/增量的指定識別屬性，引擎不會重複使用識別值。 如果特定 INSERT 陳述式失敗或此 INSERT 陳述式已回復，則取用的識別值將會遺失而且不會再次產生。 這樣在產生後續識別值時會產生間隙。  
  
 這些限制是為了提升效能之設計的一部分，而且也可在許多常見的情況中被接受。 如果您因為這些限制而無法使用識別值，請建立個別的資料表來保存目前的值，並使用您的應用程式管理資料表的存取和數字指派。  
  
 如果發行含識別欄位的資料表來進行複寫，您必須依照使用的複寫類型所適用的方式，來管理識別欄位。 如需詳細資訊，請參閱[複寫識別資料欄](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 每份資料表都只能建立一個識別欄位。  
  
 在經記憶體最佳化的資料表中，種子和增量必須設為 1,1。 若將種子或增量設為 1 以外的值，會產生下列錯誤：經記憶體最佳化的資料表不支援使用 1 以外的種子和增量值。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-the-identity-property-with-create-table"></a>A. 搭配 CREATE TABLE 使用 IDENTITY 屬性  
 下列範例會利用自動累加的識別碼之 `IDENTITY` 屬性，來建立一份新的資料表。  
  
```  
USE AdventureWorks2012;  
  
IF OBJECT_ID ('dbo.new_employees', 'U') IS NOT NULL  
   DROP TABLE new_employees;  
GO  
CREATE TABLE new_employees  
(  
 id_num int IDENTITY(1,1),  
 fname varchar (20),  
 minit char(1),  
 lname varchar(30)  
);  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Karin', 'F', 'Josephs');  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Pirkko', 'O', 'Koskitalo');  
```  
  
### <a name="b-using-generic-syntax-for-finding-gaps-in-identity-values"></a>B. 利用一般語法來尋找識別值的間距  
 下列範例會顯示在移除資料時，用來尋找識別值間距的一般語法。  
  
> [!NOTE]  
>  下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼的第一部份僅供解說之用。 您可以執行開頭是下列註解的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼：`-- Create the img table`。  
  
```  
-- Here is the generic syntax for finding identity value gaps in data.  
-- The illustrative example starts here.  
SET IDENTITY_INSERT tablename ON;  
DECLARE @minidentval column_type;  
DECLARE @maxidentval column_type;  
DECLARE @nextidentval column_type;  
SELECT @minidentval = MIN($IDENTITY), @maxidentval = MAX($IDENTITY)  
    FROM tablename  
IF @minidentval = IDENT_SEED('tablename')  
   SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('tablename')  
   FROM tablename t1  
   WHERE $IDENTITY BETWEEN IDENT_SEED('tablename') AND   
      @maxidentval AND  
      NOT EXISTS (SELECT * FROM tablename t2  
         WHERE t2.$IDENTITY = t1.$IDENTITY +   
            IDENT_INCR('tablename'))  
ELSE  
   SELECT @nextidentval = IDENT_SEED('tablename');  
SET IDENTITY_INSERT tablename OFF;  
-- Here is an example to find gaps in the actual data.  
-- The table is called img and has two columns: the first column   
-- called id_num, which is an increasing identification number, and the   
-- second column called company_name.  
-- This is the end of the illustration example.  
  
-- Create the img table.  
-- If the img table already exists, drop it.  
-- Create the img table.  
IF OBJECT_ID ('dbo.img', 'U') IS NOT NULL  
   DROP TABLE img;  
GO  
CREATE TABLE img (id_num int IDENTITY(1,1), company_name sysname);  
INSERT img(company_name) VALUES ('New Moon Books');  
INSERT img(company_name) VALUES ('Lucerne Publishing');  
-- SET IDENTITY_INSERT ON and use in img table.  
SET IDENTITY_INSERT img ON;  
  
DECLARE @minidentval smallint;  
DECLARE @nextidentval smallint;  
SELECT @minidentval = MIN($IDENTITY) FROM img  
 IF @minidentval = IDENT_SEED('img')  
    SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('img')  
    FROM img t1  
    WHERE $IDENTITY BETWEEN IDENT_SEED('img') AND 32766 AND  
      NOT    EXISTS (SELECT * FROM img t2  
          WHERE t2.$IDENTITY = t1.$IDENTITY + IDENT_INCR('img'))  
 ELSE  
    SELECT @nextidentval = IDENT_SEED('img');  
SET IDENTITY_INSERT img OFF;  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [IDENT_INCR &#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTITY &#40;函式&#41; &#40;Transact-SQL&#41;](../../t-sql/functions/identity-function-transact-sql.md)   
 [IDENT_SEED &#40;Transact-SQL&#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md)   
 [複寫識別資料行](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
