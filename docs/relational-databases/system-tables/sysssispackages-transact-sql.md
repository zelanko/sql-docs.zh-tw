---
title: "sysssispackages (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysdtspackages90_TSQL
- sysdtspackages90
dev_langs: TSQL
helpviewer_keywords: sysssispackages system table
ms.assetid: 66155dcd-dcdb-4e33-a242-1625828ad8d2
caps.latest.revision: "43"
author: spelluru
ms.author: spelluru
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5b694a277a235b373f1051878551ccca9537623f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysssispackages-transact-sql"></a>sysssispackages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含一個資料列的每個封裝儲存至[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這份資料表儲存在**msdb**資料庫。  
  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|封裝的唯一識別碼。|  
|**id**|**uniqueidentifier**|封裝的 GUID。|  
|**描述**|**nvarchar**|封裝的選擇性描述。|  
|**createdate**|**datetime**|封裝的建立日期。|  
|**folderid**|**uniqueidentifier**|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 列出封裝所在之邏輯資料夾的 GUID。|  
|**ownersid**|**varbinary**|建立封裝之使用者的唯一安全性識別碼。|  
|**packagedata**|**image**|封裝。|  
|**packageformat**|**int**|儲存封裝的格式：<br /><br /> 值為 2 表示此封裝會儲存在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]格式。<br /><br /> 值為 3 表示的格式儲存封裝[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]或更新版本。|  
|**packagetype**|**int**|建立封裝的用戶端。 可能的值如下：<br /><br /> 0 (預設值)<br /><br /> 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出精靈)<br /><br /> 3 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]複寫)<br /><br /> 5 ([!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具)<br /><br /> 6 (維護計畫設計師或精靈)。<br /><br /> <br /><br /> 請注意，此資料行中的值對應到<xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>列舉型別。|  
|**vermajor**|**int**|封裝的最新主要版本。|  
|**verminor**|**int**|封裝的最新次要版本。|  
|**verbuild**|**int**|封裝的最新組建。|  
|**vercomments**|**nvarchar**|有關封裝版本的註解。|  
|**verid**|**uniqueidentifier**|封裝版本的 GUID。|  
|**isencrypted**|**bit**|指出封裝是否加密的布林。|  
|**readrolesid**|**varbinary**|可以載入封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色。|  
|**writerolesid**|**varbinary**|可以儲存封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色。|  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services &#40;SSIS&#41; 封裝](../../integration-services/integration-services-ssis-packages.md)  
  
  
