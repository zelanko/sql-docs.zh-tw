---
title: "ISJSON (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISJSON
- ISJSON_TSQL
helpviewer_keywords:
- ISJSON function
- JSON, validating
ms.assetid: c836f3d3-3e17-44ae-92bf-f341918896c3
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b641847387801097bce59e78cf75255cc7217be
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="isjson-transact-sql"></a>ISJSON (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  測試字串是否包含有效的 JSON。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
ISJSON ( expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 要測試的字串。  
  
## <a name="return-value"></a>傳回值  
 傳回 1，如果字串包含有效的 JSON。反之則傳回 0。 傳回 null 如果*運算式*為 null。  
  
 不會傳回錯誤。  
  
## <a name="remarks"></a>備註  
 **ISJSON**不會檢查相同層級的索引鍵的唯一性。  
  
## <a name="examples"></a>範例  
  
### <a name="example-1"></a>範例 1  
下列範例會執行陳述式區塊有條件地如果參數值`@param`包含有效的 JSON。  
  
```sql  
DECLARE @param <data type>
SET @param = <value>

IF (ISJSON(@param) > 0)  
BEGIN  
     -- Do something with the valid JSON value of @param.  
END
 
```  
  
### <a name="example-2"></a>範例 2  
下列範例會傳回資料行 `json_col` 中包含有效 JSON 的資料列。  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  
  
## <a name="see-also"></a>另請參閱  
 [JSON 資料 &#40;SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

