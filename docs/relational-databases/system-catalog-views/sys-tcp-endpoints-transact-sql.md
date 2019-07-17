---
title: sys.tcp_endpoints (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.tcp_endpoints
- sys.tcp_endpoints_TSQL
- tcp_endpoints
- tcp_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.tcp_endpoints catalog view
ms.assetid: 43cc3afa-cced-4463-8e97-fbfdaf2e4fa8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7e4b711a7d36e7677f6f32b87ff4c696db231730
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116726"
---
# <a name="systcpendpoints-transact-sql"></a>sys.tcp_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對系統中每個 TCP 端點，各包含一個資料列。 所描述的端點**sys.tcp_endpoints**提供要授與及撤銷連接權限的物件。 顯示的通訊埠及 IP 位址相關資訊不會用來設定通訊協定，而且可能與實際的通訊協定組態不相符。 若要檢視及設定通訊協定，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**< 繼承的資料行 >**||繼承資料行從[sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)。|  
|**port**|ssNoversion|端點正在接聽的通訊埠編號。 不可為 Null。|  
|**is_dynamic_port**|bit|1 = 通訊埠編號是以動態方式指派。<br /><br /> 不可為 Null。|  
|**ip_address**|**nvarchar(45)**|由 LISTENER_IP 子句指定的接聽程式 IP 位址。 可為 Null。|  
  
## <a name="remarks"></a>備註  
 執行以下查詢來收集有關端點和連接的資訊。 沒有目前連接或沒有 TCP 連接的端點將以 NULL 值顯示。 新增**何處**子句`WHERE des.session_id = @@SPID`來傳回目前連接相關資訊。  
  
```  
SELECT des.login_name, des.host_name, program_name,  dec.net_transport, des.login_time,   
e.name AS endpoint_name, e.protocol_desc, e.state_desc, e.is_admin_endpoint,   
t.port, t.is_dynamic_port, dec.local_net_address, dec.local_tcp_port   
FROM sys.endpoints AS e  
LEFT JOIN sys.tcp_endpoints AS t  
   ON e.endpoint_id = t.endpoint_id  
LEFT JOIN sys.dm_exec_sessions AS des  
   ON e.endpoint_id = des.endpoint_id  
LEFT JOIN sys.dm_exec_connections AS dec  
   ON des.session_id = dec.session_id;  
```  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [端點目錄檢視&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
