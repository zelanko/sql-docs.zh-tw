---
title: "資料類型 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 9/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system data types [SQL Server]
- data types [SQL Server]
- data types [SQL Server], about data types
ms.assetid: a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: d9a995f7d29fe91e14affa9266a9bce73acc9010
ms.openlocfilehash: 75efc7b5a58b3739a196e36b2c80d4ee37a92003
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="data-types-transact-sql"></a>資料類型 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，每個資料行、區域變數、運算式和參數都有相關的資料類型。 資料類型是指定物件所能保留之資料類型的屬性，這些資料類型包括整數資料、字元資料、貨幣資料、日期和時間資料、二進位字串等。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供一組系統資料來定義搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所能使用的所有資料類型。 您也可以定義自己的資料型別中[!INCLUDE[tsql](../../includes/tsql-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]。 別名資料類型是以系統提供的資料類型為基礎。 如需有關別名資料類型的詳細資訊，請參閱[CREATE TYPE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-type-transact-sql.md). 使用者定義型別會從您利用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 支援的程式設計語言所建立之類別的方法和運算子來取得它們的性質。
  
當運算子結合的兩個運算式有不同的資料類型、定序、有效位數、小數位數或長度時，結果的性質取決於下列各點：
-   結果的資料類型，取決於輸入運算式的資料類型所套用的資料類型優先順序規則。 如需詳細資訊，請參閱[資料類型優先順序 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
-   結果的定序由定序優先順序規則的結果資料類型時**char**， **varchar**，**文字**， **nchar**， **nvarchar**，或**ntext**。 如需詳細資訊，請參閱[定序優先順序 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/collation-precedence-transact-sql.md).  
-   結果的有效位數、小數位數和長度會隨著輸入運算式的有效位數、小數位數和長度而不同。 如需詳細資訊，請參閱[有效位數、小數位數和長度 &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供 ISO 相容的資料類型同義字。 如需詳細資訊，請參閱[資料類型同義字 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
## <a name="data-type-categories"></a>資料類型類別目錄
中的資料類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]組織成下列類別：
  
|||  
|-|-|  
|精確數值|Unicode 字元字串|  
|近似數值|二進位字串|  
|日期和時間|其他資料類型|  
|字元字串||  
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，以儲存體的性質為基礎，某些資料類型指定為屬於下列群組：
-   大數值資料類型： **varchar （max)**，和**nvarchar （max)**  
-   大型物件資料類型：**文字**， **ntext**，**映像**， **varbinary （max)**，和**xml**  
  
    > [!NOTE]  
    >  sp_help 會傳回-1 做為大數值的長度和**xml**資料型別。  
  
### <a name="exact-numerics"></a>精確數值
  
|||  
|-|-|  
|[bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[numeric](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[decimal](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|[smallmoney](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)||  
  
### <a name="approximate-numerics"></a>近似數值
  
|||  
|-|-|  
|[float](../../t-sql/data-types/float-and-real-transact-sql.md)|[real](../../t-sql/data-types/float-and-real-transact-sql.md)|  
  
### <a name="date-and-time"></a>日期和時間
  
|||  
|-|-|  
|[date](../../t-sql/data-types/date-transact-sql.md)|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|[time](../../t-sql/data-types/time-transact-sql.md)|  
  
### <a name="character-strings"></a>字元字串
  
|||  
|-|-|  
|[char](../../t-sql/data-types/char-and-varchar-transact-sql.md)|[varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|[text](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="unicode-character-strings"></a>Unicode 字元字串
  
|||  
|-|-|  
|[nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|[nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
|[ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="binary-strings"></a>二進位字串
  
|||  
|-|-|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|[image](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="other-data-types"></a>其他資料類型
  
|||  
|-|-|  
|[cursor](../../t-sql/data-types/cursor-transact-sql.md)|[rowversion](../../t-sql/data-types/rowversion-transact-sql.md)|  
|[hierarchyid](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md)|  
|[sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)|[xml](../../t-sql/xml/xml-transact-sql.md)|  
|[Geometry 空間類型](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md) |[空間地理位置類型](../../t-sql/spatial-geography/spatial-types-geography.md)|  
|[table](../../t-sql/data-types/table-transact-sql.md) | |
  
## <a name="see-also"></a>另請參閱
[CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[宣告@local_variable&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 
 [EXECUTE &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/execute-transact-sql.md)  
[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[函式 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/functions.md)  
[像 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[sp_droptype &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)  
[sp_help &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)  
[sp_rename &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
  
  

