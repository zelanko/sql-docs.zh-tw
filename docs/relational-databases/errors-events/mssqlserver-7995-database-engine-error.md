---
title: MSSQLSERVER_7995 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7995 (Database Engine error)
ms.assetid: af6d6322-3cba-43d8-be97-e6ef15f8c933
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16f2bebd761898fad44cd19c78c02470420b6d18
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72906555"
---
# <a name="mssqlserver_7995"></a>MSSQLSERVER_7995
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|7995|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC2_SYSTEM_CATALOGS_CORRUPT|  
|訊息文字|資料庫 'DBNAME': 在系統目錄中的一致性錯誤導致無法進一步 DBCC CHECKNAME 處理。|  
  
## <a name="explanation"></a>說明  
DBCC CHECKDB 處理序由下列三個階段組成：  
  
1.  配置檢查。 這相當於執行 DBCC CHECKALLOC。  
  
2.  系統資料表一致性的檢查。 這相當於針對必要的系統基底資料表，執行小型清單的 DBCC CHECKTABLE。  
  
3.  完整資料庫一致性的檢查。  

MSSQLEngine_7995 在第 2 階段引發，指出 DBCC CHECKDB 已經找到命令無法修復或尚未指定 REPAIR 的錯誤。 DBCC CHECKDB 無法繼續進行第 3 階段，因為有問題的系統基底資料表儲存資料庫中所有物件的中繼資料，或是系統基底資料表已損毀。  
  
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
請檢查錯誤清單，查看 REPAIR 針對每項錯誤所執行的動作。  
  
