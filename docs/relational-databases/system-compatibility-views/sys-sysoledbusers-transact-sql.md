---
title: sys.sysoledbusers （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 331e0feea8fb0e1e7eb9637640a8bcebce3ee992
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764345"
---
# <a name="syssysoledbusers-transact-sql"></a>sys.sysoledbusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

    
> [!IMPORTANT]  
>  將這份 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 系統資料表併入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作為一份檢視的目的，只是為了與舊版相容。 我們建議您改用[目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)。  
  
 針對指定連結伺服器的每個使用者和密碼對應，各包含一個資料列。 **sysoledbusers**儲存在**master**資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**rmtsrvid**|**smallint**|伺服器的安全性識別碼 (SID)。|  
|**rmtloginame**|**Nvarchar （** 128 **）**|**Loginsid**對應至連結**rmtservid**的遠端登入名稱。|  
|**rmtpassword**|**Nvarchar （** 128 **）**|傳回 NULL。|  
|**loginsid**|**varbinary(** 85 **)**|所要對應的本機登入 SID。|  
|**status**|**smallint**|如果是 1，則對應應該使用使用者的認證。|  
|**changedate**|**datetime**|上次變更對應資訊的日期。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
