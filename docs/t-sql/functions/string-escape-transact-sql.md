---
title: STRING_ESCAPE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRING_ESCAPE
- STRING_ESCAPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_ESCAPE function
ms.assetid: 2163bc7a-3816-4304-9c40-8954804f5465
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 932d1a8be595bedf9ccdbddae854a17c4578e64a
ms.sourcegitcommit: e2d65828faed6f4dfe625749a3b759af9caa7d91
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59670834"
---
# <a name="stringescape-transact-sql"></a>STRING_ESCAPE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  逸出文字中的特殊字元並傳回逸出之字元的文字。 **STRING_ESCAPE** 是決定性函數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql
STRING_ESCAPE( text , type )  
```  
  
## <a name="arguments"></a>引數

 *text*  
 這是代表應該逸出之物件的 **nvarchar**[expression](../../t-sql/language-elements/expressions-transact-sql.md) 運算式。  
  
 *type*  
 將套用的逸出規則。 目前支援的值是 `'json'`。  
  
## <a name="return-types"></a>傳回類型

 帶有逸出的特殊與控制字元的 **nvarchar(max)** 文字。 目前，**STRING_ESCAPE** 只能逸出下表中顯示的 JSON 特殊字元。  
  
|特殊字元|編碼的序列|  
|-----------------------|----------------------|  
|引號 (")|\\"|  
|反斜線 (\\)|\\\|  
|斜線 (/)|\\/|  
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
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>範例  
  
### <a name="a--escape-text-according-to-the-json-formatting-rules"></a>A.  根據 JSON 格式化規則逸出文字

 下列查詢會使用 JSON 規則逸出特殊字元並傳回逸出的文字。  
  
```sql
SELECT STRING_ESCAPE('\   /  
\\    "     ', 'json') AS escapedText;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
escapedText  
-------------------------------------------------------------  
\\\t\/\n\\\\\t\"\t
```  
  
### <a name="b-format-json-object"></a>B. 格式化 JSON 物件

 下列查詢會從數字和字串變數建立 JSON 文字，並逸出變數中的任何特殊 JSON 字元。  
  
```
SET @json = FORMATMESSAGE('{ "id": %d,"name": "%s", "surname": "%s" }',
    17, STRING_ESCAPE(@name,'json'), STRING_ESCAPE(@surname,'json') );  
```  
  
## <a name="see-also"></a>另請參閱

 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)