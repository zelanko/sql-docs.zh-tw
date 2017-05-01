---
title: MSSQLSERVER_2522 | Microsoft Docs
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
- 2522 (Database Engine error)
ms.assetid: 19b9b00c-330f-4dd3-9052-9d88bce83849
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0b4e2e3299bd6d32b2d9cef5af9cf070f725c076
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver2522"></a>MSSQLSERVER_2522
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2522|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_INDEX_FILEGROUP_IS_INVALID|  
|訊息文字|檔案群組 F_NAME 無效，因此無法處理資料表 O_NAME 的索引 I_NAME。|  
  
## <a name="explanation"></a>說明  
這項參考用訊息指出由於儲存在索引中繼資料的其中一個檔案群組識別碼不存在，因此無法檢查索引。 無效的檔案群組識別碼可能與資料本身、大型物件 (LOB) 資料或資料列溢位資料有關。  
  
如果沒有問題，則會檢查相同物件的其他所有索引。  
  
## <a name="user-action"></a>使用者動作  
  
### <a name="look-for-hardware-failure"></a>尋找硬體故障  
請執行硬體診斷並更正所有問題， 同時檢查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 系統和應用程式記錄檔以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，以查看錯誤發生的原因是否為硬體故障。 請修正前述記錄檔中所包含的任何硬體相關問題。  
  
若有持續發生的資料損毀問題，請嘗試抽換不同的硬體元件以隔離問題。 請檢查以確認系統並未啟用磁碟控制器上的寫入快取功能。 如果您懷疑寫入快取就是問題所在，請與您的硬體廠商連絡。  
  
最後，切換到新的硬體系統可能也會有幫助。 此切換作業可能包括重新格式化磁碟機以及重新安裝作業系統。  
  
### <a name="restore-from-backup"></a>還原備份  
如果問題與硬體無關，而且確定有未受影響的備份可以使用，請利用該備份來還原資料庫。  
  
### <a name="run-dbcc-checkdb"></a>執行 DBCC CHECKDB  
不適用。 此錯誤無法自動修復。  
  

