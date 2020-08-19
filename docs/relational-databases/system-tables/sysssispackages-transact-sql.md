---
description: sysssispackages (Transact-SQL)
title: sysssispackages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackages90_TSQL
- sysdtspackages90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackages system table
ms.assetid: 66155dcd-dcdb-4e33-a242-1625828ad8d2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d1a1bda3bfea233f7a586a8147f268fbdb1e6ade
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419032"
---
# <a name="sysssispackages-transact-sql"></a>sysssispackages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對儲存至的每個封裝，各包含一個資料列 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 此資料表儲存在 **msdb** 資料庫中。  
  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|封裝的唯一識別碼。|  
|**id**|**uniqueidentifier**|封裝的 GUID。|  
|**description**|**nvarchar**|封裝的選擇性描述。|  
|**createdate**|**datetime**|封裝的建立日期。|  
|**folderid**|**uniqueidentifier**|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 列出封裝所在之邏輯資料夾的 GUID。|  
|**ownersid**|**varbinary**|建立封裝之使用者的唯一安全性識別碼。|  
|**packagedata**|**image**|封裝。|  
|**packageformat**|**int**|儲存封裝的格式：<br /><br /> 值為2表示封裝是以 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 格式儲存。<br /><br /> 值為3表示封裝是以 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或更新版本的格式儲存。|  
|**packagetype**|**int**|建立封裝的用戶端。 可能的值如下：<br /><br /> 0 (預設值)<br /><br /> 1 (匯 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 入和匯出 Wizard) <br /><br /> 3 (複寫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) <br /><br /> 5 ([!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具) <br /><br /> 6 (維護計畫設計師或精靈)。<br /><br /> <br /><br /> 請注意，這個資料行中的值會對應到 <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType> 列舉。|  
|**vermajor**|**int**|封裝的最新主要版本。|  
|**verminor**|**int**|封裝的最新次要版本。|  
|**verbuild**|**int**|封裝的最新組建。|  
|**vercomments**|**nvarchar**|有關封裝版本的註解。|  
|**verid**|**uniqueidentifier**|封裝版本的 GUID。|  
|**isencrypted**|**bit**|指出封裝是否加密的布林。|  
|**readrolesid**|**varbinary**|可以載入封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色。|  
|**writerolesid**|**varbinary**|可以儲存封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色。|  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 封裝](../../integration-services/integration-services-ssis-packages.md)  
  
  
