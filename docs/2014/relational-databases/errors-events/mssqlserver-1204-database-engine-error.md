---
title: MSSQLSERVER_1204 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1204 (Database Engine error)
ms.assetid: de6ece78-79de-484d-9224-ca0f7645815f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee0544c14bbf3e05fcb59e16a9bb3e0d8e61e33b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916099"
---
# <a name="mssqlserver1204"></a>MSSQLSERVER_1204
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|1204|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LK_OUTOF|  
|訊息文字|SQL Server Database Engine 的執行個體目前無法取得 LOCK 資源。 請在使用中使用者較少時重新執行您的陳述式。 要求資料庫管理員檢查這個執行個體的鎖定與記憶體組態，或者檢查長時間執行的交易。|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法取得鎖定資源。 這項錯誤可能是由於下列其中一個原因所造成：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法從作業系統配置更多記憶體，原因可能是其他處理序正在使用作業系統，或是因為伺服器正在運作，而且已經設定 **max server memory** 選項。  
  
-   鎖定管理員不會使用超過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可用記憶體的 60%。  
  
## <a name="user-action"></a>使用者動作  
 如果您懷疑 SQL Server 無法配置足夠的記憶體，請嘗試下列方法：  
  
-   如果有 SQL Server 以外的應用程式正在耗用資源，請嘗試停止這些應用程式或考慮在不同的伺服器上執行這些應用程式。 這個動作可以從 SQL Server 的其他處理序釋出記憶體。  
  
-   如果您已經設定 max server memory，請增加 max server memory 的設定值。  
  
 如果您懷疑鎖定管理員已經使用最大的可用記憶體容量，請找出擁有最大鎖定數量的交易，並結束該筆交易。 下列指令碼會找出擁有最大鎖定數量的交易：  
  
```  
SELECT request_session_id, COUNT (*) num_locks  
FROM sys.dm_tran_locks  
GROUP BY request_session_id   
ORDER BY count (*) DESC  
```  
  
 取得最高的工作階段識別碼，並使用 KILL 命令結束該工作階段。  
  
  
