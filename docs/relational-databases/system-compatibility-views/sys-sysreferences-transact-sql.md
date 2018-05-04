---
title: (TRANSACT-SQL) 的 sys.sysreferences |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sysreferences
- sys.sysreferences_TSQL
- sysreferences
- sysreferences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysreferences compatibility view
- sysreferences system table
ms.assetid: 81276f13-202e-4e74-962d-46eb98c98d2e
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 85892a9153039d6e3a4ef3e8c0caa0cdf667db55
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="syssysreferences-transact-sql"></a>sys.sysreferences (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  包含 FOREIGN KEY 條件約束定義與資料庫內參考資料行的對應。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|FOREIGN KEY 條件約束的識別碼。|  
|**fkeyid**|**int**|參考資料表的識別碼。|  
|**rkeyid**|**int**|被參考資料表的識別碼。|  
|**rkeyindid**|**smallint**|參考資料表上的唯一索引之索引識別碼，涵蓋參考索引鍵資料行。|  
|**keycnt**|**smallint**|索引鍵中的資料行數。|  
|**forkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**refkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**fkeydbid**|**smallint**|已保留。|  
|**rkeydbid**|**smallint**|已保留。|  
|**fkey1**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey2**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey3**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey4**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey5**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey6**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey7**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey8**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey9**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey10**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey11**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey12**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey13**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey14**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey15**|**smallint**|參考資料行的資料行識別碼。|  
|**fkey16**|**smallint**|參考資料行的資料行識別碼。|  
|**rkey1**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey2**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey3**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey4**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey5**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey6**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey7**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey8**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey9**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey10**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey11**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey12**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey13**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey14**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey15**|**smallint**|被參考之資料行的資料行識別碼。|  
|**rkey16**|**smallint**|被參考之資料行的資料行識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視表&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
