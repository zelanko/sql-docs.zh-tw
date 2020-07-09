---
title: MSSQLSERVER_8651 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8651 (Database Engine error)
ms.assetid: 4cc3498d-5449-4c4e-b1f9-3271831c725a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7a28655b2f86c02b1985196c05c16b866e3e0897
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637126"
---
# <a name="mssqlserver_8651"></a>MSSQLSERVER_8651
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
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
  
2.  開始收集下列項目的效能監視器計數：**SQL Server：緩衝區管理員**、**SQL Server：記憶體管理員**。  
  
3.  檢查下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體組態參數：  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
    注意不尋常的設定， 並且視需要加以更正。 預設值列於《SQL Server 線上叢書》中的＜設定伺服器組態選項＞。  
  
4.  檢查工作負載 (例如，並行工作階段的數目以及目前正在執行的查詢數)。  

下列動作可以為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供更多可用的記憶體：  
  
-   如果有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外的應用程式正在耗用資源，請嘗試停止執行這些應用程式或考慮在不同的伺服器上執行這些應用程式。 這將會移除外部的記憶體壓力。  
  
-   如果已經設定 **max server memory,** ，請增加其設定值。  
  
執行下列 DBCC 命令，以便釋放數個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體快取。  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
如果仍繼續發生該問題，您必須進一步研究，而且可能必須降低工作負載。  
  
## <a name="see-also"></a>另請參閱  
[DBCC FREESYSTEMCACHE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)  
[DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[伺服器組態選項 &#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md)  
[SQL Server 的 Buffer Manager 物件](~/relational-databases/performance-monitor/sql-server-buffer-manager-object.md)  
[SQL Server 的 Memory Manager 物件](~/relational-databases/performance-monitor/sql-server-memory-manager-object.md)  
  
