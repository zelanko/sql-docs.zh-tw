---
title: 可用性群組的 SQL Server 資源 DLL 健全狀況診斷記錄
description: 描述 SQL Server 資源 DLL 如何監視 Always On 可用性群組的健全狀況。
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: c1862d8a-5f82-4647-a280-3e588b82a6dc
author: rothja
ms.author: jroth
manager: jroth
ms.openlocfilehash: f9df88d021ffa6aebbc30f3a733ece3b395ac102
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66789588"
---
# <a name="sql-server-resource-dll-health-diagnostic-logs-for-availability-groups"></a>可用性群組的 SQL Server 資源 DLL 健全狀況診斷記錄
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  由 Windows Server 容錯移轉叢集 (WSFC) 叢集執行的 SQL Server 資源 DLL 會使用 SQL Server 執行個體中稱為 [sp_server_diagnostics](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 的預存程序，來監視主要可用性複本的健康情況。  
  
 SQL Server 資源 DLL 會維持與 SQL Server 執行個體的專用開啟連線，SQL Server 執行個體可透過該連線定期將詳細健康情況診斷傳送到 SQL Server 資源 DLL。 結合健康情況診斷和叢集中在可用性群組資源內設定的容錯移轉原則 (FailoverConditionLevel 屬性)，可供叢集用來判斷要重新啟動或是要對可用性群組資源進行容錯移轉。 SQL Server 2012 和更新版本執行個體使用此預存程序傳送活動訊號到 WSFC 叢集，它比 SQL Server 2008 R2 或舊版中的更為繫為細微且可靠，因為它使用查詢 `SELECT @@SERVERNAME` 建立與執行個體的定期連線。 然後您可以設定可用性群組 FailureConditonLevel 屬性，以控制觸發容錯移轉的條件。  
  
 **使用 SQL Server 容錯移轉叢集診斷記錄**
 
 SQL Server 資源 DLL 從 sp_server_diagnostics 接收到的所有健康情況診斷，都自動儲存到 SQL Server 執行個體的預設 [Log] 目錄中 (%PROGRAMFILES%\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Log)。 這些記錄檔稱為 SQLDIAG 記錄檔，且以 XEL (擴充事件) 檔案格式儲存。 這些檔案在 SQL Server 的 [Log] 目錄中具有下列格式：\<主機名稱>_\<執行個體名稱>_SQLDIAG_X_XXXXXXXXX.xel。 藉由查看 SQLDIAG 記錄檔，您或許可以判斷可用性群組資源失敗或容錯移轉事件的根本原因。  
  
 若要檢視 SQLDIAG 記錄檔，請將 .xel 檔案拖曳至 SQL Server Management Studio 中。  
  
  
