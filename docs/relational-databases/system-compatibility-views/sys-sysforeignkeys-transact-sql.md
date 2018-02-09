---
title: "sys.sysforeignkeys (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysforeignkeys
- sys.sysforeignkeys
- sys.sysforeignkeys_TSQL
- sysforeignkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysforeignkeys system table
- sys.sysforeignkeys compatibility view
ms.assetid: 41544236-1c46-4501-be88-18c06963b6e8
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9cdf2d4dd70f5d4894b1f6a3a671171e7c59c667
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="syssysforeignkeys-transact-sql"></a>sys.sysforeignkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含在資料庫表格定義中的 FOREIGN KEY 條件約束的相關資訊。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|FOREIGN KEY 條件約束的識別碼。|  
|**fkeyid**|**int**|具有 FOREIGN KEY 條件約束之資料表的物件識別碼。|  
|**rkeyid**|**int**|FOREIGN KEY 條件約束中所參考之資料表的物件識別碼。|  
|**fkey**|**smallint**|參考資料行的識別碼。|  
|**rkey**|**smallint**|被參考之資料行的識別碼。|  
|**keyno**|**smallint**|參考資料行清單中的資料行位置。|  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
