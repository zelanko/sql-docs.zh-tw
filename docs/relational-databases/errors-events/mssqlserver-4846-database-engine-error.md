---
title: MSSQLSERVER_4846 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 4846 (Database Engine error)
ms.assetid: a455e809-1883-4c7d-b3e3-835ee5bfe258
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 04c787695e92763f32fb940ce7491f8119a6244f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver4846"></a>MSSQLSERVER_4846
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|4846|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|BULKPROV_MEMORY|  
|訊息文字|大量資料提供者無法配置記憶體。|  
  
## <a name="explanation"></a>說明  
記憶體配置失敗。  
  
## <a name="user-action"></a>使用者動作  
請遵循下列一般步驟以疑難排解記憶體錯誤：  
  
1.  確認是否有其他應用程式或服務正在耗用此伺服器的記憶體。 重新設定比較不重要的應用程式或服務，以降低其記憶體耗用量。  
  
2.  開始收集 **SQL Server: Buffer Manager** 和 **SQL Server: Memory Manager** 的效能監視器計數器。  
  
3.  檢查下列 SQL Server 記憶體組態參數：  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
    注意不尋常的設定， 並且視需要加以更正。 說明 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的記憶體需求。 預設值列於《SQL Server 線上叢書》中的＜設定伺服器組態選項＞。  
  
4.  當您看到這些錯誤訊息時，請觀察 DBCC MEMORYSTATUS 輸出以及它變更的方式。  
  
5.  檢查工作負載 (例如，並行工作階段的數目以及目前正在執行的查詢數)。  
  
下列動作可以為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供更多可用的記憶體：  
  
-   如果有 SQL Server 以外的應用程式正在耗用資源，請嘗試停止執行這些應用程式或考慮在不同的伺服器上執行這些應用程式。 這將會移除外部的記憶體壓力。  
  
-   如果已經設定 **max server memory,**，請增加其設定值。  
  
執行下列 DBCC 命令，以便釋放數個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體快取。  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
如果仍繼續發生該問題，您必須進一步研究，而且可能必須降低工作負載。  
  
