---
title: MSSQLSERVER_2534 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2534 (Database Engine error)
ms.assetid: 121cf99d-0722-494c-be24-3369c1a0badc
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e9c5636a4ad7b5e2def8c246d2f03e58dcf3e8f5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver2534"></a>MSSQLSERVER_2534
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|2534|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_PAGE_ALLOCATED_TO_OTHER_OBJECT|  
|訊息文字|資料表錯誤: 頁面 P_ID (其標頭顯示是配置給物件識別碼 O_ID)，索引識別碼 I_ID，分割區識別碼 PN_ID，配置單位識別碼 A_ID (類型 TYPE)，是由其他物件所配置。|  
  
## <a name="explanation"></a>說明  
頁面標頭包含配置單位識別碼 (*A_ID*)，但是該配置單位中並無配置此頁面的索引配置對應 (IAM) 頁面。 因此，頁面的標頭包含錯誤的配置單位識別碼，並且頁面上將會顯示相符的 MSSQLServer_2533 錯誤，而該錯誤會對應到此頁面實際配置的配置單位識別碼。  
  
## <a name="user-action"></a>使用者動作  
  
### <a name="look-for-hardware-failure"></a>尋找硬體故障  
請執行硬體診斷並更正所有問題， 同時檢查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 系統和應用程式記錄檔以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，以查看錯誤發生的原因是否為硬體故障。 請修正前述記錄檔中所包含的任何硬體相關問題。  
  
若有持續發生的資料損毀問題，請嘗試抽換不同的硬體元件以隔離問題。 請檢查以確認系統並未啟用磁碟控制器上的寫入快取功能。 如果您懷疑寫入快取就是問題所在，請與您的硬體廠商連絡。  
  
最後，切換到新的硬體系統可能也會有幫助。 此切換作業可能包括重新格式化磁碟機以及重新安裝作業系統。  
  
### <a name="restore-from-backup"></a>還原備份  
如果問題與硬體無關，而且確定有未受影響的備份可以使用，請利用該備份來還原資料庫。  
  
### <a name="run-dbcc-checkdb"></a>執行 DBCC CHECKDB  
如果沒有未受影響的備份可以使用，請執行不含 REPAIR 子句的 DBCC CHECKDB，以確定損毀的範圍。 DBCC CHECKDB 將建議適用的 REPAIR 子句。 接著，請執行內含適當 REPAIR 子句的 DBCC CHECKDB，以修復損毀的部分。  
  
> [!CAUTION]  
> 如果不確定內含 REPAIR 子句之 DBCC CHECKDB 的效果為何，執行此陳述式之前請先與主要支援提供者連絡。  
  
如果執行含 REPAIR 子句的 DBCC CHECKDB 並未修正這個問題，請與您的主要支援提供者連絡，再執行這個陳述式。  
  
### <a name="results-of-running-repair-options"></a>執行 REPAIR 選項的結果  
如果索引存在，REPAIR 便會重建索引。  
  
> [!CAUTION]  
> 若針對相符的 [MSSQLSERVER_2533](~/relational-databases/errors-events/mssqlserver-2533-database-engine-error.md) 錯誤執行 REPAIR，則會先取消配置頁面再進行重建。  
  
> [!CAUTION]  
> 此修復可能會導致資料遺失。  
  
