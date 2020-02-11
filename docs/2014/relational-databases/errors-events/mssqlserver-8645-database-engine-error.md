---
title: MSSQLSERVER_8645 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8645 (Database Engine error)
ms.assetid: 63d6d6d7-3850-4061-8e96-b1fa665e3180
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7a039055daf8574d0c6b217c26d6f5572dd015c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62762560"
---
# <a name="mssqlserver_8645"></a>MSSQLSERVER_8645
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|8645|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|MEMTIMEDOUT_ERR|  
|訊息文字|等候記憶體資源來執行查詢時發生逾時。 請重新執行查詢。|  
  
## <a name="explanation"></a>說明  
 等候記憶體資源來執行資源集區 'default' 中的查詢時發生逾時。  
  
## <a name="user-action"></a>使用者動作  
 如果您未使用資源管理員，我們建議您對整個伺服器狀態和負載進行驗證，或者檢查資源集區或工作負載群組設定。  
  
 下列清單概述有助於疑難排解記憶體錯誤的一般步驟：  
  
1.  確認是否有其他應用程式或服務正在耗用此伺服器的記憶體。 重新設定比較不重要的應用程式或服務，以降低其記憶體耗用量。  
  
2.  開始收集 **SQL Server: Buffer Manager** 和 **SQL Server: Memory Manager** 的效能監視器計數器。  
  
3.  檢查下列 SQL Server 記憶體組態參數：  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
     注意不尋常的設定， 並且視需要加以更正。 說明 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的增加記憶體需求。 預設值列於《SQL Server 線上叢書》中的＜設定伺服器組態選項＞。  
  
4.  當您看到這些錯誤訊息時，請觀察 DBCC MEMORYSTATUS 輸出以及它變更的方式。  
  
5.  檢查工作負載 (例如，並行工作階段的數目以及目前正在執行的查詢數)。  
  
 下列動作可以為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供更多可用的記憶體：  
  
-   如果有 SQL Server 以外的應用程式正在耗用資源，請嘗試停止執行這些應用程式或考慮在不同的伺服器上執行這些應用程式。 這將會移除外部的記憶體壓力。  
  
-   如果已經設定 **max server memory,** ，請增加其設定值。  
  
 執行下列 DBCC 命令，以釋放數個 SQL Server 記憶體快取。  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 如果仍繼續發生該問題，您必須進一步研究，而且可能必須降低工作負載。  
  
  
