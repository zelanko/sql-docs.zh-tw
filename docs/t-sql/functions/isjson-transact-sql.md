---
title: ISJSON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ISJSON
- ISJSON_TSQL
helpviewer_keywords:
- ISJSON function
- JSON, validating
ms.assetid: c836f3d3-3e17-44ae-92bf-f341918896c3
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 9b98e7250f6cea54401ba533c769ab2be0bc82cf
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65577562"
---
# <a name="isjson-transact-sql"></a>ISJSON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

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
 若字串包含有效的 JSON，則傳回 1；否則傳回 0。 若 *expression* 為 null，則傳回 null。  
  
 不會傳回錯誤。  
  
## <a name="remarks"></a>Remarks  
 **ISJSON** 不會檢查相同層級中索引鍵的唯一性。  
  
## <a name="examples"></a>範例  
  
### <a name="example-1"></a>範例 1  
下列範例會在參數值 `@param` 包含有效的 JSON 時條件式的執行陳述式區塊。  
  
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
 [JSON 資料 &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
