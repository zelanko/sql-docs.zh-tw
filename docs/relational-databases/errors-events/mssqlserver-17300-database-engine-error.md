---
title: MSSQLSERVER_17300 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17300 (Database Engine error)
ms.assetid: c1d6bfb6-28af-4df6-8087-25807602d282
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ef809a200d3544e5e24549440506b77d6f1a79e5
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver17300"></a>MSSQLSERVER_17300
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|17300|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PROC_OUT_OF_SYSTASK_SESSIONS|  
|訊息文字|由於記憶體不足或設定的工作階段數目超過伺服器的容許最大值，使 SQL Server 無法執行新的系統工作。 請確認伺服器是否有足夠的記憶體。 使用 sp_configure 搭配 'user connections' 選項來檢查允許的最大使用者連接數目。 使用 sys.dm_exec_sessions 來檢查目前的工作階段數目，包括使用者處理。|  
  
## <a name="explanation"></a>說明  
嘗試執行新系統工作的行為失敗，因為記憶體不足，或者超過了伺服器的已設定工作階段數目。  
  
## <a name="user-action"></a>使用者動作  
請確認伺服器擁有足夠的記憶體。 請使用 sys.dm_exec_sessions 來確認目前的系統工作數目，並且使用 sp_configure 來確認最大使用者連接的設定值。  
  
依照需要執行下列工作：  
  
-   為伺服器增加更多記憶體。  
  
-   結束一個或多個工作階段。  
  
-   增加伺服器允許的最大使用者連接數目。  
  
## <a name="see-also"></a>另請參閱  
[sp_configure &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
[伺服器組態選項 &#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md)  
[sys.dm_exec_sessions &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[設定 user connections 伺服器組態選項](~/database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
[KILL &#40;Transact-SQL&#41;](~/t-sql/language-elements/kill-transact-sql.md)  
  

