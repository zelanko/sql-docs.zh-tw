---
title: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: c2dd0389f4ec3287fbe23875458ab5d34ef269f7
ms.sourcegitcommit: 79e6d49ae4632f282483b0be935fdee038f69cc2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2019
ms.locfileid: "72174652"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

顯示 Azure [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 資料庫的已使用儲存空間結果集快取。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  
## <a name="remarks"></a>Remarks

`DBCC SHOWRESULTCACHESPACEUSED` 命令不接受任何參數，而且會傳回命令執行所在資料庫的已使用空間。

結果集快取的大小上限是每個資料庫 1 TB。  Azure SQL 資料倉儲會自動撤出結果集快取中的項目：

- 若結果集尚未使用，則為每 48 小時撤出一次。
- 當結果集快取接近大小上限時。

若要手動清空資料庫的結果集快取，使用者可以使用下列其中一個選項：

- 關閉資料庫的結果集快取功能
- 在連線到資料庫的情況下執行 `DBCC DROPRESULTSETCACHE` 

暫停資料庫將不會清空結果集快取。  

## <a name="permissions"></a>權限

需要 VIEW SERVER STATE 權限。
  
## <a name="result-sets"></a>結果集  
  
|資料行|資料類型|Description|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|資料庫使用的總空間 (KB)。 當快取的結果集增加時，此數字就會變更。|  
|data_space|BIGINT|資料使用的空間 (KB)。|  
|index_space|BIGINT|索引使用的空間 (KB)。|  
|unused_space|BIGINT|保留未使用的空間 (KB)。|  


## <a name="see-also"></a>另請參閱

[ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE  &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)