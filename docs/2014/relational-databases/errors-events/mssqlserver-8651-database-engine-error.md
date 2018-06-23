---
title: MSSQLSERVER_8651 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 8651 (Database Engine error)
ms.assetid: 4cc3498d-5449-4c4e-b1f9-3271831c725a
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 14ab756575298042c19a7d53ace5c41055392836
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023108"
---
# <a name="mssqlserver8651"></a>MSSQLSERVER_8651
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|8651|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|MEMGRANT_ERR|  
|訊息文字|無法進行要求的作業，因為最小的查詢記憶體無法使用。 請降低 'min memory per query' 伺服器設定選項的設定值。|  
  
## <a name="explanation"></a>說明  
 有其他處理序正在耗用伺服器記憶體 (造成伺服器的記憶體壓力)。  
  
## <a name="user-action"></a>使用者動作  
 減少 'min memory per query' 伺服器組態選項的值，或減少伺服器的查詢負載。  
  
 下列清單概述有助於疑難排解記憶體錯誤的一般步驟：  
  
1.  確認是否有其他應用程式或服務正在耗用此伺服器的記憶體。 重新設定比較不重要的應用程式或服務，以降低其記憶體耗用量。  
  
2.  開始收集 **SQL Server: Buffer Manager** 和 **SQL Server: Memory Manager** 的效能監視器計數器。  
  
3.  檢查下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體組態參數：  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
     注意不尋常的設定， 並且視需要加以更正。 預設值列於《SQL Server 線上叢書》中的＜設定伺服器組態選項＞。  
  
4.  檢查工作負載 (例如，並行工作階段的數目以及目前正在執行的查詢數)。  
  
 下列動作可以為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供更多可用的記憶體：  
  
-   如果有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外的應用程式正在耗用資源，請嘗試停止執行這些應用程式或考慮在不同的伺服器上執行這些應用程式。 這將會移除外部的記憶體壓力。  
  
-   如果已經設定 **max server memory,**，請增加其設定值。  
  
 執行下列 DBCC 命令，以便釋放數個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體快取。  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 如果仍繼續發生該問題，您必須進一步研究，而且可能必須降低工作負載。  
  
## <a name="see-also"></a>另請參閱  
 [DBCC FREESYSTEMCACHE &#40;Transact SQL&#41;](/sql/t-sql/database-console-commands/dbcc-freesystemcache-transact-sql)   
 [DBCC FREESESSIONCACHE &#40;Transact SQL&#41;](/sql/t-sql/database-console-commands/dbcc-freesessioncache-transact-sql)   
 [DBCC FREEPROCCACHE &#40;Transact SQL&#41;](/sql/t-sql/database-console-commands/dbcc-freeproccache-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [SQL Server 的 Buffer Manager 物件](../performance-monitor/sql-server-buffer-manager-object.md)   
 [SQL Server 的 Memory Manager 物件](../performance-monitor/sql-server-memory-manager-object.md)  
  
  
