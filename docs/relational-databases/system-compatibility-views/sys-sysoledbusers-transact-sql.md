---
title: sys.sysoledbusers (TRANSACT-SQL) |Microsoft 文件
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
- sys.sysoledbusers
- sys.sysoledbusers_TSQL
- sysoledbusers
- sysoledbusers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoledbusers system table
- sys.sysoledbusers compatibility view
ms.assetid: fe924c17-9cad-4b2b-8124-1e0fd82931e3
caps.latest.revision: 34
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9bed55c42d7d656f53e24acb1d859658666ce901
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33220839"
---
# <a name="syssysoledbusers-transact-sql"></a>sys.sysoledbusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  將這份 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 系統資料表併入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作為一份檢視的目的，只是為了與舊版相容。 我們建議您改用[目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)改為。  
  
 針對指定連結伺服器的每個使用者和密碼對應，各包含一個資料列。 **sysoledbusers**會儲存在**主要**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**rmtsrvid**|**smallint**|伺服器的安全性識別碼 (SID)。|  
|**rmtloginame**|**nvarchar(** 128 **)**|遠端登入名稱的**loginsid**連結會對應至**rmtservid**。|  
|**rmtpassword**|**nvarchar(** 128 **)**|傳回 NULL。|  
|**loginsid**|**varbinary(** 85 **)**|所要對應的本機登入 SID。|  
|**status**|**smallint**|如果是 1，則對應應該使用使用者的認證。|  
|**changedate**|**datetime**|上次變更對應資訊的日期。|  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
