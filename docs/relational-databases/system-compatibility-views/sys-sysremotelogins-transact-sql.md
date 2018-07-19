---
title: sys.sysremotelogins (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysremotelogins
- sysremotelogins_TSQL
- sys.sysremotelogins
- sys.sysremotelogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysremotelogins system table
- sys.sysremotelogins compatibility view
ms.assetid: b7ffcfa6-aed8-41d4-8b70-845439ab813d
caps.latest.revision: 35
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 37778d98343a3b897b2957a718dd32001892931d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "33222743"
---
# <a name="syssysremotelogins-transact-sql"></a>sys.sysremotelogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含一個資料列，每個遠端使用者允許的執行個體呼叫遠端預存程序[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**remoteserverid**|**smallint**|遠端伺服器識別。|  
|**remoteusername**|**sysname**|遠端伺服器的使用者登入名稱。|  
|**status**|**smallint**|傳回 0。|  
|**sid**|**varbinary(85)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者安全性識別碼。|  
|**changedate**|**datetime**|加入遠端使用者的日期和時間。|  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視表&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
