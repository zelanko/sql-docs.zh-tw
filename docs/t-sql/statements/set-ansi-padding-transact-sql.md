---
title: SET ANSI_PADDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a463063777f27a50d7edb81450df5c6de4720a53
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37782009"
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

SET ANSI_PADDING ON
```

## <a name="remarks"></a>Remarks  
 以 **char**、**varchar**、**binary** 和 **varbinary** 資料類型定義的資料行具有定義的大小。  
  
 這項設定只會影響新資料行的定義。 建立好資料行之後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據建立資料行之時的設定來儲存值。 這項設定後來的變更並不會影響現有的資料行。  
  
> [!NOTE]  
>  我們建議您一律將 ANSI_PADDING 設為 ON。  
  
 下表顯示當值插入含 **char**、**varchar**、**binary** 和 **varbinary** 等資料類型的資料行時，SET ANSI_PADDING 設定所造成的影響。  
  
|設定|char(*n*) NOT NULL 或 binary(*n*) NOT NULL|char(*n*) NULL 或 binary(*n*) NULL|varchar(*n*) 或 varbinary(*n*)|  
|-------------|----------------------------------------------------|--------------------------------------------|----------------------------------------|  
|ON|將原始值填補到資料行的長度 (**char** 資料行使用尾端空格，**binary** 資料行使用尾端零)。|當 SET ANSI_PADDING 是 ON 時，請遵照 **char(***n***)** 或 **binary(***n***)** NOT NULL 的相同規則。|不修剪插入 **varchar** 資料行之字元值的尾端空格。 不修剪插入 **varbinary** 資料行之二進位值的尾端零。 值不會填補到資料行的長度。|  
|OFF|將原始值填補到資料行的長度 (**char** 資料行使用尾端空格，**binary** 資料行使用尾端零)。|當 SET ANSI_PADDING 是 OFF 時，請遵照 **varchar** 或 **varbinary** 的相同規則。|修剪插入 **varchar** 資料行之字元值的尾端空格。 修剪插入 **varbinary** 資料行之二進位值的尾端零。|  
  
> [!NOTE]  
>  當填補時，**char** 資料行會填補空格，**binary** 資料行會填補零。 當修剪時，**char** 資料行會修剪尾端空格，**binary** 資料行會修剪尾端零。  
  
 當您建立或變更計算資料行索引或索引檢視表時，SET ANSI_PADDING 也必須是 ON。 如需使用索引檢視表和計算資料行索引時所需之 SET 選項設定的詳細資訊，請參閱 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md) 中的＜使用 SET 陳述式時的考量＞一節。  
  
 SET ANSI_PADDING 的預設值是 ON。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者在連接時，都會自動將 ANSI_PADDING 設為 ON。 在連接之前，您可以在應用程式的 ODBC 資料來源、ODBC 連接屬性或 OLE DB 連接屬性集中設定這個項目。 起始於 DB-Library 應用程式的連接之 SET ANSI_PADDING 預設值為 OFF。  
  
 SET ANSI_PADDING 設定不會影響 **nchar**、**nvarchar**、**ntext**、**text**、**image**、**varbinary(max)**、**varchar(max)** 和 **nvarchar(max)** 資料型別。 它們一律會顯示 SET ANSI_PADDING ON 行為。 這表示不會修剪尾端空格和零。  
  
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
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  
