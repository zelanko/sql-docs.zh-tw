---
title: H (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdistpublishers
- MSdistpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistpublishers system table
ms.assetid: 31844099-4b33-4dc9-84b4-bac70aa82598
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5da07fa3d9f2214a2ec325c0f83739be497895a4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  **MSdistpublishers**資料表針對本機散發者所支援的每個遠端發行者包含一個資料列。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|發行集散發者的名稱。|  
|**distribution_db**|**sysname**|散發資料庫的名稱。|  
|**working_directory**|**nvarchar(255)**|用來儲存發行集資料和結構描述檔案的工作目錄名稱。|  
|**security_mode**|**int**|在散發者端實作的安全性模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。<br /><br /> **1** = Windows 驗證。|  
|**login**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。|  
|**password**|**nvarchar （524)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼 (加密)。|  
|**使用中**|**bit**|指出本機散發者是否正由遠端發行者所使用。|  
|**受信任**|**bit**|指出遠端發行者所用的密碼，是否與本機散發者一樣：<br /><br /> **0** = A 遠端發行者連接到 「 散發者 」 需要密碼。<br /><br /> **1** = 否需要密碼。|  
|**third_party**|**bit**|發行者是否為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一項安裝：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝。**1** = 異質資料來源。|  
|**publisher_type**|**sysname**|發行者類型：<br /><br /> **MSSQLSERVER**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。<br /><br /> **ORACLE** = 標準 Oracle 發行者。<br /><br /> **ORACLE GATEWAY** = Oracle Gateway 發行者。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
