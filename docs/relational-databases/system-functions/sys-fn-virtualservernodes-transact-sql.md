---
title: sys.fn_virtualservernodes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_virtualservernodes
- fn_virtualservernodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- nodes [Faillover Clustering], virtual servers
- nodes [Faillover Clustering]
- virtual servers [Faillover Clustering]
- failover clustering [SQL Server], nodes
- fn_virtualservernodes function
- sys.fn_virtualservernodes function
ms.assetid: 257f3b8d-93c0-4444-87f1-ea211bd8cad0
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4073c1668ef43e7d303a3e534d16763d33939e45
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38042786"
---
# <a name="sysfnvirtualservernodes-transact-sql"></a>sys.fn_virtualservernodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可在其中執行的容錯移轉叢集執行個體節點清單。 在容錯移轉叢集環境中，這項資訊非常有用。  
  
> [!IMPORTANT]  
>  這[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]系統函式是為了回溯相容性。 我們建議您改用[sys.dm_os_cluster_nodes &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
fn_virtualservernodes()  
```  
  
## <a name="tables-returned"></a>傳回的資料表  
 如果目前的伺服器是叢集的伺服器， **fn_virtualservernodes**傳回的容錯移轉叢集執行個體節點清單，這個執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已定義。  
  
 如果目前的伺服器執行個體不是叢集的伺服器， **fn_virtualservernodes**傳回空的資料列集。  
  
## <a name="permissions"></a>Permissions  
 使用者必須有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會利用 `fn_virtualservernodes` 來查詢叢集伺服器執行個體：  
  
```  
SELECT * FROM fn_virtualservernodes();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 NodeName  
  
 -------\-  
  
 SS3-CLUSN1  
  
 SS3-CLUSN2  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_os_cluster_nodes &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys.fn_servershareddrives &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)  
  
  
