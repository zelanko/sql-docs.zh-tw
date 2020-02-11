---
title: sysssispackages （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 21487ba46e53997ebb50403cc4eaf1ae54f0a103
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029637"
---
# <a name="sysssispackages-transact-sql"></a>sysssispackages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對儲存到[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每個封裝，各包含一個資料列。 此資料表會儲存在**msdb**資料庫中。  
  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|封裝的唯一識別碼。|  
|**號**|**uniqueidentifier**|封裝的 GUID。|  
|**描述**|**nvarchar**|封裝的選擇性描述。|  
|**createdate**|**datetime**|封裝的建立日期。|  
|**folderid**|**uniqueidentifier**|
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 列出封裝所在之邏輯資料夾的 GUID。|  
|**ownersid**|**varbinary**|建立封裝之使用者的唯一安全性識別碼。|  
|**packagedata**|**image**|封裝。|  
|**packageformat**|**int**|儲存封裝的格式：<br /><br /> 值為2表示封裝是以[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]格式儲存。<br /><br /> 值為3表示封裝是以或更新版本的[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]格式儲存。|  
|**packagetype**|**int**|建立封裝的用戶端。 可能的值如下：<br /><br /> 0 (預設值)<br /><br /> 1（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出嚮導）<br /><br /> 3（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]複寫）<br /><br /> 5（[!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具）<br /><br /> 6 (維護計畫設計師或精靈)。<br /><br /> <br /><br /> 請注意，此資料行中的值會<xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>對應到列舉。|  
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
  
  
