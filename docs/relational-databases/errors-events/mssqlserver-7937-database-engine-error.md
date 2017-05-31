---
title: MSSQLSERVER_7937 | Microsoft Docs
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
- 7937 (Database Engine error)
ms.assetid: 7dcc61a3-975d-4662-8a4e-c153e26b36c6
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c1e232906b95fea88ff713cfa5d38d5381fc5585
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver7937"></a>MSSQLSERVER_7937
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|7937|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC2_FS_MISSING_COLUMN_DIRECTORY|  
|訊息文字|資料表錯誤: 找不到物件識別碼 O_ID，索引識別碼 I_ID，分割區識別碼 PN_ID 中資料行識別碼 C_ID 的 FileStream 目錄。|  
  
## <a name="explanation"></a>說明  
指定的資料行存在於分割區中；不過，在 FILESTREAM 資料空間中找不到其對應的 FILESTREAM 目錄。  
  
## <a name="user-action"></a>使用者動作  
  
### <a name="look-for-hardware-failure"></a>尋找硬體故障  
請執行硬體診斷並更正所有問題， 同時檢查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 系統和應用程式記錄檔以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，以查看錯誤發生的原因是否為硬體故障。 請修正前述記錄檔中所包含的任何硬體相關問題。  
  
若有持續發生的資料損毀問題，請嘗試抽換不同的硬體元件以隔離問題。 請檢查以確認系統並未啟用磁碟控制器上的寫入快取功能。 如果您懷疑寫入快取就是問題所在，請與您的硬體廠商連絡。  
  
最後，切換到新的硬體系統可能也會有幫助。 此切換作業可能包括重新格式化磁碟機以及重新安裝作業系統。  
  
### <a name="restore-from-backup"></a>還原備份  
如果問題與硬體無關，而且確定有未受影響的備份可以使用，請利用該備份來還原資料庫。  
  
### <a name="run-dbcc-checkdb"></a>執行 DBCC CHECKDB  
不適用。 此錯誤無法自動修復。 如果無法從備份還原資料庫，請連絡 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客戶服務及支援中心 (CSS)。  
  

