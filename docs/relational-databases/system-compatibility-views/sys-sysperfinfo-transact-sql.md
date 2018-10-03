---
title: sys.sysperfinfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysperfinfo_TSQL
- sys.sysperfinfo_TSQL
- sys.sysperfinfo
- sysperfinfo
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysperfinfo compatibility view
- sysperfinfo system table
ms.assetid: e22a81cd-27de-4690-9443-6aad6393bd3c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 954ad81a9bbc2c2a76e825a944a292b00e478218
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47596697"
---
# <a name="syssysperfinfo-transact-sql"></a>sys.sysperfinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的 Windows 系統監視器所能顯示之內部效能計數器的表示法。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|效能物件名稱，例如**SQLServer:LockManager**或是**SQLServer:BufferManager**。|  
|**counter_name**|**nchar(128)**|在物件中，效能計數器的名稱這類**網頁要求**或是**要求的鎖定數**。|  
|**instance_name**|**nchar(128)**|計數器的具名執行個體。 比方說，都會維護若干計數器每種類型的鎖定，這類**表格**，**頁面**，**金鑰**，依此類推。 相似計數器的執行個體名稱各不相同。|  
|**cntr_value**|**bigint**|實際的計數器值。 這通常都是一個層級計數器或單純增加的計數器，用來計算執行個體事件的出現次數。|  
|**cntr_type**|**int**|Windows 效能架構所定義的計數器類型。|  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視表&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
