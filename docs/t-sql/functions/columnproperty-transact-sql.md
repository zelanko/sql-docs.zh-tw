---
title: "COLUMNPROPERTY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLUMNPROPERTY
- COLUMNPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- parameters [SQL Server], properties
- COLUMNPROPERTY function
ms.assetid: 2408c264-6eca-4120-bb71-df043c7c2792
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: c6c2af8d231f03c40ee87d3468977c3b66cbeeb4
ms.contentlocale: zh-tw
ms.lasthandoff: 10/05/2017

---
# <a name="columnproperty-transact-sql"></a>COLUMNPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回資料行或參數的相關資訊。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
COLUMNPROPERTY ( id , column , property )   
```  
  
## <a name="arguments"></a>引數  
*id*  
是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，其中包含的資料表或程序的識別碼 (ID)。
  
*資料行*  
這是包含資料行或參數名稱的運算式。
  
*屬性*  
是包含要傳回之資訊的運算式*識別碼*，而且可以是下列值之一。
  
|值|Description|傳回的值|  
|---|---|---|
|**AllowsNull**|允許 Null 值|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**ColumnId**|對應至資料行識別碼值**sys.columns.column_id**。|資料行識別碼<br /><br /> **注意：**時查詢多個資料行，資料行識別碼值的序列可能會有間距。|  
|**FullTextTypeColumn**|行文件類型資訊的資料表中的 [類型] 欄*資料行*。|這個屬性的第二個參數所傳遞的資料行全文檢索 TYPE COLUMN 識別碼。|  
|**IsComputed**|資料行是一個計算資料行。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**IsCursorType**|程序參數的類型是 CURSOR。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**Columnproperty**|資料行具有決定性。 這個屬性只適用於計算資料行和檢視資料行。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。 不是計算資料行或檢視資料行。|  
|**IsFulltextIndexed**|資料行已完成全文檢索索引的登錄。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**IsIdentity**|資料行使用 IDENTITY 屬性。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**IsIdNotForRepl**|資料行會檢查 IDENTITY_INSERT 設定。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**IsIndexable**|資料行可以建立索引。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**IsOutParam**|程序參數是一個輸出參數。|1 = TRUE<br /><br /> 0 = FALSE NULL = 輸入無效。|  
|**IsPrecise**|資料行是精確的。 這個屬性只適用於具決定性的資料行。|1 = TRUE<br /><br /> 0 = FALSE NULL = 輸入無效。 不是具決定性的資料行|  
|**IsRowGuidCol**|資料行具有**uniqueidentifier**資料型別且具有 ROWGUIDCOL 屬性定義。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**IsSystemVerified**|您可以利用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 來驗證資料行的決定性和有效位數屬性。 這個屬性只適用於計算資料行和檢視資料行。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**IsXmlIndexable**|XML 資料行可用於 XML 索引中。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**有效位數**|資料行或參數的資料類型長度。|指定的資料行資料類型長度<br /><br /> -1 = **xml**或大數值類型<br /><br /> NULL = 輸入無效。|  
|**小數位數**|資料行或參數的資料類型小數位數。|小數位數<br /><br /> NULL = 輸入無效。|  
|**StatisticalSemantics**|資料行啟用語意索引。|1 = TRUE<br /><br /> 0 = FALSE|  
|**SystemDataAccess**|資料行是從存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統目錄或虛擬系統資料表中之資料的函數衍生而來。 這個屬性只適用於計算資料行和檢視資料行。|1 = TRUE (表示唯讀存取。)<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**UserDataAccess**|資料行是從存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機執行個體所儲存的使用者資料表 (包括檢視和暫存資料表) 中之資料的函數衍生而來。 這個屬性只適用於計算資料行和檢視資料行。|1 = TRUE (表示唯讀存取。)<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效。|  
|**UsesAnsiTrim**|在最初建立資料表時，ANSI_PADDING 設為 ON。 這個屬性只適用於資料行或參數的型別**char**或**varchar**。|1= TRUE <br /><br /> 0= FALSE <br /><br /> NULL = 輸入無效。|  
|**IsSparse**|資料行是疏鬆資料行。 如需詳細資訊，請參閱 [使用疏鬆資料行](../../relational-databases/tables/use-sparse-columns.md)。|1= TRUE <br /><br /> 0= FALSE <br /><br /> NULL = 輸入無效。|  
|**IsColumnSet**|資料行是資料行集。 如需詳細資訊，請參閱 [使用資料行集](../../relational-databases/tables/use-column-sets.md)。|1= TRUE <br /><br /> 0= FALSE <br /><br /> NULL = 輸入無效。|  
|**GeneratedAlwaysType**|由系統產生的資料行值。 對應至**sys.columns.generated_always_type**|**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 0 = 未產生一律<br /><br /> 1 = 一律為資料列開始的產生<br /><br /> 2 – 一律產生資料列結尾為|  
|**IsHidden**|由系統產生的資料行值。 對應至**sys.columns.is_hidden**|**適用於**： [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 0 = 未隱藏<br /><br /> 1 = 隱藏|  
  
## <a name="return-types"></a>傳回型別
 **int**  
  
## <a name="exceptions"></a>例外狀況  
當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。
  
使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，COLUMNPROPERTY) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。
  
## <a name="remarks"></a>備註  
當您檢查資料行的決定性屬性時，請先測試資料行是否為計算資料行。 **Columnproperty**是非計算資料行，則傳回 NULL。 您可以將計算資料行指定成索引資料行。
  
## <a name="examples"></a>範例  
下列範例會傳回 `LastName` 資料行的長度。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT COLUMNPROPERTY( OBJECT_ID('Person.Person'),'LastName','PRECISION')AS 'Column Length';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Column Length
-------------
50
```  
  
## <a name="see-also"></a>另請參閱
[中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[TYPEPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)
  
  

