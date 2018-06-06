---
title: sys.dm_os_cluster_nodes (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes
- sys.dm_os_cluster_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_cluster_nodes dynamic management view
ms.assetid: 92fa804e-2d08-42c6-a36f-9791544b1d42
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6fb5b957cfdaa340ec90a9bb30a5e9db6a54ca31
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmosclusternodes-transact-sql"></a>sys.dm_os_cluster_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對容錯移轉叢集執行個體組態中之每個節點傳回一個資料列。 如果目前的執行個體就是容錯移轉叢集執行個體，將會傳回定義有此容錯移轉叢集執行個體 (先前稱為「虛擬伺服器」) 之節點的清單。 如果目前的伺服器執行個體不是容錯移轉叢集執行個體，它會傳回空的資料列集。  
  
> **注意：** 呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_cluster_nodes**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**NodeName**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體 (虛擬伺服器) 組態中的節點名稱。|  
|status|**int**|中的節點狀態[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]容錯移轉叢集執行個體： 0、 1、 2、 3、-1。 如需詳細資訊，請參閱[GetClusterNodeState 函數](http://go.microsoft.com/fwlink/?LinkId=204794)。|  
|status_description|**nvarchar(20)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集節點狀態的說明。<br /><br /> 0 = 啟動<br /><br /> 1 = 關閉<br /><br /> 2 = 暫停<br /><br /> 3 = 正在加入<br /><br /> 1 = 未知|  
|is_current_owner|bit|1 表示這個節點是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集資源的目前擁有者。|  
|pdw_node_id|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="remarks"></a>備註  
 當啟用容錯移轉叢集時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體 (虛擬伺服器) 組態所指定之一部分的任何容錯移轉叢集節點中執行。  
  
> **注意：** 這個檢視會取代在未來版本將會被取代的 fn_virtualservernodes 函數。  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會使用 sys。 dm_os_cluster_nodes 傳回位於叢集伺服器執行個體上的節點。  
  
```  
SELECT NodeName, status, status_description, is_current_owner   
FROM sys.dm_os_cluster_nodes;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|NodeName|status|status_description|is_current_owner|  
|--------------|------------|-------------------------|------------------------|  
|node1|0|啟動|1|  
|node2|0|啟動|0|  
|Node3|1|關閉|0|  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_os_cluster_properties &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-properties-transact-sql.md)   
 [sys.dm_io_cluster_shared_drives &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [sys.fn_virtualservernodes &#40;Transact SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  



