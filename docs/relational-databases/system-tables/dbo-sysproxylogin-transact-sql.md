---
description: dbo.sysproxylogin (Transact-SQL)
title: dbo.sysproxylogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxylogin_TSQL
- sysproxylogin_TSQL
- dbo.sysproxylogin
- sysproxylogin
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxylogin system table
ms.assetid: 433d33cb-bdf2-47bb-af78-2a40b7c8dfce
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bafbc9a0e8712d0d81bed477e21f6932f3a47694
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446601"
---
# <a name="dbosysproxylogin-transact-sql"></a>dbo.sysproxylogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  記錄與每個 SQL Server Agent Proxy 帳戶相關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 此資料表儲存在 **msdb** 資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶的識別碼。 這個值會對應至**sysproxies**資料表中的**proxy_id**資料行。|  
|**希**|**Varbinary (85) **|適用于 SQL Server 登入的 Microsoft Windows *security_identifier* 。|  
|**principal_id**|**int**|有權使用指定子系統步驟的 Proxy 帳戶之使用者或群組的識別碼。|  
|**flags**|**int**|登入類型：<br /><br /> **0** = Windows 使用者或群組，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。<br /><br /> **1**個  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定系統角色<br /><br /> **2**  = **msdb**資料庫角色|  
  
## <a name="remarks"></a>備註  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠存取此資料表。  
  
## <a name="see-also"></a>另請參閱  
 [dbo.sys&#40;Transact-sql&#41;的 proxy ](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
