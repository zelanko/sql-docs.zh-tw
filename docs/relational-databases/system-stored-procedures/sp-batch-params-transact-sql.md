---
title: sp_batch_params (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_batch_params
- sp_batch_params_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_batch_params
ms.assetid: 7b92fe9e-e755-4b7a-8a15-822c58a813d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b66e8b2d1b0d397a24c4ff5c702c00aff14988d4
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492810"
---
# <a name="spbatchparams-transact-sql"></a>sp_batch_params (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回包含資訊中包括的參數資料列集[!INCLUDE[tsql](../../includes/tsql-md.md)]批次。 **sp_batch_params**只會剖析指定的批次，且會傳回內嵌的參數值的相關資訊。 它不會執行批次或修改執行環境。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_batch_params [ [ @tsqlbatch = ] 'tsqlbatch' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @tsqlbatch = ] 'tsqlbatch'` 是 Unicode 字串，包含[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式或批次參數是您想要的資訊。 *tsqlbatch*已**nvarchar （max)** 或隱含地轉換成**nvarchar （max)**。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**PARAMETER_NAME**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在批次中找到的參數名稱。|  
|**COLUMN_TYPE**|**smallint**|這個欄位會傳回下列其中一個值：<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE<br /><br /> 這個資料行一律是 0。|  
|**DATA_TYPE**|**smallint**|參數的資料類型 (ODBC 資料類型的整數碼)。 如果這個資料類型無法對應至 ISO 類型，此值就是 NULL。 原生資料型別名稱都會傳入**TYPE_NAME**資料行。 這個值一律是 NULL。|  
|**TYPE_NAME**|**sysname**|依照基礎 DBMS 所代表的資料類型字串表示法。 這個值是 NULL。|  
|**PRECISION**|**int**|有效位數的數目。 傳回值**精確度**資料行是在基底為 10。|  
|**LENGTH**|**int**|資料的傳送大小。 這個值是 NULL。|  
|**SCALE**|**smallint**|小數點右側的位數。 這個值是 NULL。|  
|**RADIX**|**smallint**|這是數值類型的基底。 這個值是 NULL。|  
|**可為 NULL**|**smallint**|指定 Null 屬性：<br /><br /> 1 = 參數資料類型可以建立成允許 Null 值。<br /><br /> 0 = 不允許 Null 值。<br /><br /> 這個值是 NULL。|  
|**SQL_DATA_TYPE**|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型出現在描述子 TYPE 欄位時的值。 除了 **datetime** 和 **ISO interval** 資料類型，這個資料行與 **DATA_TYPE** 資料行相同。 這個資料行一律會傳回值。 這個值是 NULL。|  
|**SQL_DATETIME_SUB**|**smallint**|**Datetime**或 ISO**間隔**子代碼，如果值**SQL_DATA_TYPE**是 SQL_DATETIME 或 SQL_INTERVAL。 資料類型以外**datetime**和 ISO**間隔**，此資料行是 NULL。 這個值是 NULL。|  
|**CHAR_OCTET_LENGTH**|**int**|以位元組為單位的最大長度**字元**或是**二進位**資料型別參數。 所有其他資料類型的這個資料行都會傳回 NULL。 這個值一律是 NULL。|  
|**ORDINAL_POSITION**|**int**|參數在批次中的序數位置。 如果參數名稱重複許多次，這個資料行會包含第一個出現項目的序數。 第一個參數的序數為 1。 這個資料行一律會傳回值。|  
  
## <a name="permissions"></a>Permissions  
 若要執行的權限**sp_batch_params**授與**公用**。  
  
## <a name="examples"></a>範例  
 下列範例會顯示傳給 `sp_batch_params` 的查詢。 結果集會列舉內嵌參數值的清單。  
  
```  
DECLARE @SQLString nvarchar(500);  
/* Build the SQL string */  
SET @SQLString =  
     N'SELECT * FROM AdventureWorks2012.HumanResources.Employee   
     WHERE BusinessEntityID = @BusinessEntityID';  
EXECUTE sp_batch_params @SQLString;  
```  
  
## <a name="see-also"></a>另請參閱  
 [執行預存程序](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [執行預存程序的使用說明主題&#40;ODBC&#41;](https://msdn.microsoft.com/library/c2220182-a23d-4475-b353-77a77ab613d6)   
 [執行預存程序 &#40; OLE DB &#41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)  
  
  
