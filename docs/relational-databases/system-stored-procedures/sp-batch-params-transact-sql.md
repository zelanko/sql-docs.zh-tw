---
title: sp_batch_params （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 9a5b4ac7c5e1e8d3c136f99475fa7a17ebd8b002
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68001815"
---
# <a name="sp_batch_params-transact-sql"></a>sp_batch_params (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回資料列集，其中包含[!INCLUDE[tsql](../../includes/tsql-md.md)]批次中所包含之參數的相關資訊。 **sp_batch_params**只會剖析指定的批次，並傳回內嵌參數值的相關資訊。 它不會執行批次或修改執行環境。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_batch_params [ [ @tsqlbatch = ] 'tsqlbatch' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @tsqlbatch = ] 'tsqlbatch'`這是一個 Unicode 字串，其中[!INCLUDE[tsql](../../includes/tsql-md.md)]包含您想要的參數資訊所屬的語句或批次。 *tsqlbatch*是**Nvarchar （max）** 或可隱含轉換為**Nvarchar （max）**。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**PARAMETER_NAME**|**sysname**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在批次中找到的參數名稱。|  
|**COLUMN_TYPE**|**smallint**|這個欄位會傳回下列其中一個值：<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE<br /><br /> 這個資料行一律是 0。|  
|**DATA_TYPE**|**smallint**|參數的資料類型 (ODBC 資料類型的整數碼)。 如果這個資料類型無法對應至 ISO 類型，此值就是 NULL。 原生資料類型名稱會在**TYPE_NAME**資料行中傳回。 這個值一律是 NULL。|  
|**TYPE_NAME**|**sysname**|依照基礎 DBMS 所代表的資料類型字串表示法。 這個值是 NULL。|  
|**精密**|**int**|有效位數的數目。 **PRECISION**資料行的傳回值以基底10為底數。|  
|**長**|**int**|資料的傳送大小。 這個值是 NULL。|  
|**尺度**|**smallint**|小數點右側的位數。 這個值是 NULL。|  
|**RADIX**|**smallint**|這是數值類型的基底。 這個值是 NULL。|  
|**Null**|**smallint**|指定 Null 屬性：<br /><br /> 1 = 參數資料類型可以建立成允許 Null 值。<br /><br /> 0 = 不允許 Null 值。<br /><br /> 這個值是 NULL。|  
|**SQL_DATA_TYPE**|**smallint**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型出現在描述子 TYPE 欄位時的值。 除了**datetime**和 ISO **interval**資料類型之外，這個資料行與**DATA_TYPE**資料行相同。 這個資料行一律會傳回值。 這個值是 NULL。|  
|**SQL_DATETIME_SUB**|**smallint**|如果**SQL_DATA_TYPE**的值為 SQL_DATETIME 或 SQL_INTERVAL，則為**datetime**或 ISO **interval**子代碼。 若為**datetime**和 ISO **interval**以外的資料類型，這個資料行就是 Null。 這個值是 NULL。|  
|**CHAR_OCTET_LENGTH**|**int**|**字元**或**二進位**資料類型參數的最大長度（以位元組為單位）。 所有其他資料類型的這個資料行都會傳回 NULL。 這個值一律是 NULL。|  
|**ORDINAL_POSITION**|**int**|參數在批次中的序數位置。 如果參數名稱重複許多次，這個資料行會包含第一個出現項目的序數。 第一個參數的序數為 1。 這個資料行一律會傳回值。|  
  
## <a name="permissions"></a>權限  
 執行**sp_batch_params**的許可權會授與**public**。  
  
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
 [執行預存程式](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [執行預存程式的 how to 主題 &#40;ODBC&#41;](https://msdn.microsoft.com/library/c2220182-a23d-4475-b353-77a77ab613d6)   
 [執行預存程式 &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)  
  
  
