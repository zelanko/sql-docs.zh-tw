---
title: "STRING_ESCAPE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 02/25/2016
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
- STRING_ESCAPE
- STRING_ESCAPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_ESCAPE function
ms.assetid: 2163bc7a-3816-4304-9c40-8954804f5465
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 41f969e292eff76c9a836ccd3177519d88e355ac
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stringescape-transact-sql"></a>STRING_ESCAPE (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  逸出特殊字元，在文字，並傳回以逸出字元的文字。 **STRING_ESCAPE**是具決定性函數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
STRING_ESCAPE( text , type )  
```  
  
## <a name="arguments"></a>引數  
 *text*  
 是**nvarchar**[運算式](../../t-sql/language-elements/expressions-transact-sql.md)運算式應該逸出表示的物件。  
  
 *type*  
 將套用的逸出規則。 目前支援的值是`'json'`。  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar （max)**逸出的特殊和控制字元的文字。 目前**STRING_ESCAPE**只能逸出 JSON 下表所示的特殊字元。  
  
|特殊字元|編碼的序列|  
|-----------------------|----------------------|  
|引號 (")|\\"|  
|反向斜線 (\\)|\\\|  
|斜線 （/）|\\/|  
|退格鍵|\b|  
|換頁字元|\f|  
|新行|\n|  
|歸位字元|\r|  
|水平 Tab 鍵|\t|  
  
|控制字元|編碼的序列|  
|-----------------------|----------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="remarks"></a>備註  
  
## <a name="examples"></a>範例  
  
### <a name="a--escape-text-according-to-the-json-formatting-rules"></a>A.  逸出根據格式規則的 JSON 文字  
 下列查詢會逸出特殊字元使用 JSON 規則，並傳回逸出的文字。  
  
```  
SELECT STRING_ESCAPE('\   /  
\\    "     ', 'json') AS escapedText;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
escapedText  
-------------------------------------------------------------  
\\\t\/\n\\\\\t\"\t
```  
  
### <a name="b-format-json-object"></a>B. 格式的 JSON 物件  
 下列查詢會從數字和字串的變數，建立 JSON 文字並逸出任何特殊的 JSON 字元變數中。  
  
```  
SET @json = FORMATMESSAGE('{ "id": %d,"name": "%s", "surname": "%s" }',   
    17, STRING_ESCAPE(@name,'json'), STRING_ESCAPE(@surname,'json') );  
```  
  
## <a name="see-also"></a>另請參閱  
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [子字串 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
  
  

