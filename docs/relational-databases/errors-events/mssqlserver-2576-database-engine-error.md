---
title: MSSQLSERVER_2576 | Microsoft Docs
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
- 2576 (Database Engine error)
ms.assetid: b727cc2f-c76c-46f8-bbbe-5e7a05a6eabf
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b96de1b2a8056f4b88ba6df9259607e0d94aa427
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2576"></a>MSSQLSERVER_2576
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2576|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_IAM_PARENT_PAGE_WAS_NOT_SEEN|  
|訊息文字|物件識別碼 O_ID 中的索引配置對應 (IAM) 頁面 P_ID1 (索引識別碼 I_ID，分割區識別碼 PN_ID，配置單位識別碼 A_ID (類型 TYPE)) 的上一個指標指向 IAM 頁面 P_ID1，但是掃描中未偵測到這個頁面。|  
  
## <a name="explanation"></a>說明  
雖然有頁面參考可以做為 IAM 鏈結中其他 IAM 頁面的上一頁連結，但是卻找不到索引配置對應 (IAM) 頁面或中繼資料項目。 如果 *P_ID1* 頁面是 (0:0)，IAM 頁面 *P_ID2* 就是 IAM 鏈結的起點，而遺漏了 IAM 鏈結的中繼資料項目。  
  
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
REPAIR 將會嘗試重建包含 *P_ID2* 頁面的 IAM 鏈結。 重建此鏈結可能包括從鏈結中移除頁面，或是移除整個鏈結 (如果中繼資料已損毀)。  
  
> [!CAUTION]  
> 此修復可能會導致資料遺失。  
  

