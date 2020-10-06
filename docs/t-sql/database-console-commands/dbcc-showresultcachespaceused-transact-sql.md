---
description: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)
title: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7ccf83be0519d693e53154448bd36bf02f03bb52
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721949"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

顯示 Azure [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 資料庫的已使用儲存空間結果集快取。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```syntaxsql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="remarks"></a>備註

`DBCC SHOWRESULTCACHESPACEUSED` 命令不接受任何參數，而且會傳回命令執行所在資料庫的已使用空間。

## <a name="permissions"></a>權限

需要 VIEW SERVER STATE 權限。
  
## <a name="result-sets"></a>結果集  
  
|資料行|資料類型|描述|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|資料庫使用的總空間 (KB)。 當快取的結果集增加時，此數字就會變更。|  
|data_space|BIGINT|資料使用的空間 (KB)。|  
|index_space|BIGINT|索引使用的空間 (KB)。|  
|unused_space|BIGINT|保留未使用的空間 (KB)。|  

## <a name="see-also"></a>另請參閱

[使用結果集快取進行效能微調](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE  &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)
