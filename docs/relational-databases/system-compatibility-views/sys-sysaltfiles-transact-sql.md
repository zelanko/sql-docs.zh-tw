---
title: sysaltfiles （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysaltfiles_TSQL
- sys.sysaltfiles
- sysaltfiles_TSQL
- sysaltfiles
dev_langs:
- TSQL
helpviewer_keywords:
- sysaltfiles system table
- sys.sysaltfiles compatibility view
ms.assetid: 698dec23-5336-4108-87a5-f8e407f8da09
author: rothja
ms.author: jroth
ms.openlocfilehash: 891e88761cac47be83fb69debbbc5e4cb6c401c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006971"
---
# <a name="syssysaltfiles-transact-sql"></a>sys.sysaltfiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在特殊情況之下，包含對應於資料庫中之檔案的資料列。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|檔案識別碼。 每個資料庫的這個項目都是唯一的。|  
|**groupid**|**smallint**|檔案群組識別碼。|  
|**容量**|**int**|檔案大小 (以 8 KB 頁面為單位)。|  
|**maxsize**|**int**|最大檔案大小 (以 8 KB 頁面為單位)。<br /><br /> 0 = 不成長。<br /><br /> -1 = 檔案會成長到磁碟已滿。<br /><br /> 268435456 = 記錄檔可以成長到最大 2 TB 的大小。<br /><br /> 注意：使用無限制記錄檔大小進行升級的資料庫，會報告-1，表示記錄檔的大小上限。|  
|**growth**|**int**|資料庫的成長大小。<br /><br /> 0 = 不成長。 隨著狀態值而不同，它可以是頁數或檔案大小百分比。 若**狀態**為0x100000，**成長**為檔案大小的百分比;否則，它是頁面的數目。|  
|**狀態**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**效能**|**int**|已保留。|  
|**dbid**|**smallint**|這個檔案所屬的資料庫之資料庫識別碼。|  
|**name**|**sysname**|檔案的邏輯名稱。|  
|**名稱**|**nvarchar(260)**|實體裝置的名稱。 其中包括檔案的完整路徑。|  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的相容性檢視](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
