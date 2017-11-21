---
title: "SET ANSI_PADDING (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ANSI_PADDING_TSQL
- ANSI_PADDING
- SET_ANSI_PADDING_TSQL
- SET ANSI_PADDING
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], short values
- ANSI_PADDING option
- short values [SQL Server]
- SET ANSI_PADDING statement
- trailing blanks
ms.assetid: 92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 426cbfe673bafe6e1770745ca16ba23fd068fb67
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansipadding-transact-sql"></a>SET ANSI_PADDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  控制資料行針對數值長度短於資料行所定義大小的儲存方式，以及資料行針對 **char**、 **varchar**、 **binary**和 **varbinary** 資料尾端具有空白之數值的儲存方式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server  
  
SET ANSI_PADDING { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_PADDING ON;  
```  
  
## <a name="remarks"></a>備註  
 定義之資料行**char**， **varchar**，**二進位**，和**varbinary**資料型別有定義的大小。  
  
 這項設定只會影響新資料行的定義。 建立好資料行之後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據建立資料行之時的設定來儲存值。 這項設定後來的變更並不會影響現有的資料行。  
  
> [!NOTE]  
>  我們建議您一律將 ANSI_PADDING 設為 ON。  
  
 下表顯示 SET ANSI_PADDING 設定作用的資料行中插入值時**char**， **varchar**，**二進位**，和**varbinary**資料型別。  
  
|設定|char (*n*) 不為 NULL 或 binary (*n*) NOT NULL|char (*n*) NULL 或 binary (*n*) NULL|varchar (*n*) 或 varbinary (*n*)|  
|-------------|----------------------------------------------------|--------------------------------------------|----------------------------------------|  
|ON|原始值填補 (使用尾端空格**char**資料行和使用尾端的零**二進位**資料行) 的資料行長度。|遵循相同規則**char (***n***)**或**二進位 (**  *n* **)** SET ANSI_PADDING 是 ON 時，不是 NULL。|中插入的字元值尾端空格**varchar**資料行不會修剪。 之插入的二進位值尾端零**varbinary**資料行不會修剪。 值不會填補到資料行的長度。|  
|OFF|原始值填補 (使用尾端空格**char**資料行和使用尾端的零**二進位**資料行) 的資料行長度。|遵循相同規則**varchar**或**varbinary**當 SET ANSI_PADDING 是 OFF。|中插入的字元值尾端空格**varchar**資料行，則會修剪。 之插入的二進位值尾端零**varbinary**資料行，則會修剪。|  
  
> [!NOTE]  
>  當填補時， **char**資料行會填補空格，和**二進位**資料行會填補零。 當修剪時， **char**資料行具有修剪尾端空格，和**二進位**資料行具有修剪尾端零。  
  
 當您建立或變更計算資料行索引或索引檢視表時，SET ANSI_PADDING 也必須是 ON。 計算資料行上使用索引檢視表和索引的必要 SET 選項設定的相關資訊，請參閱"考量當您使用 SET 陳述式 」，在[SET 陳述式 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
 SET ANSI_PADDING 的預設值是 ON。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]都會自動將 ANSI_PADDING 設為 ON，連接時。 在連接之前，您可以在應用程式的 ODBC 資料來源、ODBC 連接屬性或 OLE DB 連接屬性集中設定這個項目。 起始於 DB-Library 應用程式的連接之 SET ANSI_PADDING 預設值為 OFF。  
  
 SET ANSI_PADDING 設定不會影響**nchar**， **nvarchar**， **ntext**，**文字**，**映像**， **varbinary （max)**， **varchar （max)**，和**nvarchar （max)**資料型別。 它們一律會顯示 SET ANSI_PADDING ON 行為。 這表示不會修剪尾端空格和零。  
  
 當 SET ANSI_DEFAULTS 是 ON 時，會啟用 SET ANSI_PADDING。  
  
 SET ANSI_PADDING 的設定是在執行時間或執行階段進行設定，而不是在剖析階段進行設定。  
  
 若要檢視此設定的目前設定，請執行下列查詢。  
  
```  
DECLARE @ANSI_PADDING VARCHAR(3) = 'OFF';  
IF ( (16 & @@OPTIONS) = 16 ) SET @ANSI_PADDING = 'ON';  
SELECT @ANSI_PADDING AS ANSI_PADDING;  
  
```  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例顯示設定如何影響這些資料類型。  
  
```  
PRINT 'Testing with ANSI_PADDING ON'  
SET ANSI_PADDING ON;  
GO  
  
CREATE TABLE t1 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t1 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t1 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '\<',  
   varbinarycol  
FROM t1;  
GO  
  
PRINT 'Testing with ANSI_PADDING OFF';  
SET ANSI_PADDING OFF;  
GO  
  
CREATE TABLE t2 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t2 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t2 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '<',  
   varbinarycol  
FROM t2;  
GO  
  
DROP TABLE t1;  
DROP TABLE t2;  
```  
  
## <a name="see-also"></a>另請參閱  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  

