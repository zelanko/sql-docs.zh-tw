---
title: "sys.sysservers (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sysservers
- sysservers_TSQL
- sysservers
- sys.sysservers_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sysservers system table
- sys.sysservers compatibility view
ms.assetid: d02f186f-c00f-44a6-b38d-dc78a3d2145b
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e05b06dd6a37f6330f715b374e3fe46515c3f37d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="syssysservers-transact-sql"></a>sys.sysservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體能夠將它當做 OLE DB 資料來源進行存取的每部伺服器，各包含一個資料列。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**srvid**|**smallint**|遠端伺服器的識別碼 (只適用於本機環境)。|  
|**srvstatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|伺服器的名稱。|  
|**srvproduct**|**sysname**|遠端伺服器的產品名稱。|  
|**providername**|**nvarchar （128)**|存取這部伺服器的 OLE DB 提供者名稱。|  
|**資料來源**|**nvarchar(4000)**|OLE DB 資料來源值。|  
|**位置**|**nvarchar(4000)**|OLE DB 位置值。|  
|**providerstring**|**nvarchar(4000)**|OLE DB 提供者字串值。|  
|**schemadate**|**datetime**|上次更新這個資料列的日期。|  
|**topologyx**|**int**|未使用。|  
|**topologyy**|**int**|未使用。|  
|**類別目錄**|**sysname**|當建立通往 OLE DB 提供者的連接時所用的目錄。|  
|**srvcollation**|**sysname**|伺服器的定序。|  
|**connecttimeout**|**int**|伺服器連接的逾時值設定。|  
|**querytimeout**|**int**|針對伺服器進行查詢的逾時值設定。|  
|**srvnetname**|**char （30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = 伺服器是遠端伺服器。<br /><br /> 0 = 伺服器是連結伺服器。|  
|**rpc**|**bit**|1 =  **sp_serveroption@rpc** 設**true**或**上**。<br /><br /> 0 =  **sp_serveroption@rpc** 設**false**或**關閉**。|  
|**pub**|**bit**|1 =  **sp_serveroption@pub** 設**true**或**上**。<br /><br /> 0 =  **sp_serveroption@pub** 設**false**或**關閉**。|  
|**sub**|**bit**|1 =  **sp_serveroption@sub** 設**true**或**上**。<br /><br /> 0 =  **sp_serveroption@sub** 設**false**或**關閉**。|  
|**dist**|**bit**|1 =  **sp_serveroption@dist** 設**true**或**上**。<br /><br /> 0 =  **sp_serveroption@dist** 設**false**或**關閉**。|  
|**dpub**|**bit**|1 =  **sp_serveroption@dpub** 設**true**或**上**。<br /><br /> 0 =  **sp_serveroption@dpub** 設**false**或**關閉**。|  
|**rpcout**|**bit**|1 =  **sp_serveroption@rpc出**設**true**或**上**。<br /><br /> 0 =  **sp_serveroption@rpc出**設**false**或**關閉**。|  
|**資料存取**|**bit**|1 =  **sp_serveroption@data存取**設**true**或**上**。<br /><br /> 0 =  **sp_serveroption@data存取**設**false**或**關閉**。|  
|**collationcompatible**|**bit**|1 =  **sp_serveroption@collation相容**設**true**或**上**。<br /><br /> 0 =  **sp_serveroption@collation相容**設**false**或**關閉**。|  
|**系統**|**bit**|1 =  **sp_serveroption@system** 設**true**或**上**。<br /><br /> 0 =  **sp_serveroption@system** 設**false**或**關閉**。|  
|**useremotecollation**|**bit**|1 =  **sp_serveroption@remote定序**設**true**或**上**。<br /><br /> 0 =  **sp_serveroption@remote定序**設**false**或**關閉**。|  
|**lazyschemavalidation**|**bit**|1 =  **sp_serveroption@lazy結構描述驗證**設**true**或**上**。<br /><br /> 0 =  **sp_serveroption@lazy結構描述驗證**設**false**或**關閉**。|  
|**定序**|**sysname**|所設定的伺服器定序**sp_serveroption@collation名稱**。|  
|**nonsqlsub**|bit|0 = 伺服器是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體<br /><br /> 1 = 伺服器不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體|  
  
## <a name="see-also"></a>請參閱＜  
 [將系統資料表對應至系統檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
