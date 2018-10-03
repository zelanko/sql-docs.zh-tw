---
title: MSSQLSERVER_824 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 824 (Database Engine error)
ms.assetid: 2aa22246-2712-4fdb-9744-36e7e6f3175e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: baf815460951a91daad76df814cd32298d49a9fa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48208318"
---
# <a name="mssqlserver824"></a>MSSQLSERVER_824
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|824|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|B_HARDSSERR|  
|訊息文字|SQL Server 偵測到邏輯的一致性 I/O 錯誤: %ls。 這是當在檔案 '%ls' 中位移 %#016I64x 的資料庫識別碼 %d 之頁面 %S_PGID 進行 %S_MSG 的期間所發生的。  SQL Server 錯誤記錄檔和系統事件記錄檔中的訊息，或許可以提供其他詳細資訊。|  
  
## <a name="explanation"></a>說明  
 此錯誤表示 Windows 回報從磁碟成功讀取頁面，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發現頁面錯誤。 此錯誤與錯誤 823 類似，不同的是 Windows 並未偵測到此錯誤。 這通常表示 I/O 子系統發生問題，例如磁碟機故障、磁碟韌體問題、錯誤的裝置驅動程式等。 如需 I/O 錯誤的詳細資訊，請參閱[Microsoft SQL Server I/O Basics, Chapter 2](http://go.microsoft.com/fwlink/?LinkId=69370) (第 2 章 Microsoft SQL Server I/O 基本概念)。  
  
## <a name="user-action"></a>使用者動作  
  
### <a name="look-for-hardware-failure"></a>尋找硬體故障  
 請執行硬體診斷並更正所有問題， 同時檢查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 系統和應用程式記錄檔以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，以查看錯誤發生的原因是否為硬體故障。 請修正前述記錄檔中所包含的任何硬體相關問題。  
  
 若有持續發生的資料損毀問題，請嘗試抽換不同的硬體元件以隔離問題。 請檢查以確認系統並未啟用磁碟控制器上的寫入快取功能。 如果您懷疑寫入快取就是問題所在，請與您的硬體廠商連絡。  
  
 最後，切換到新的硬體系統可能也會有幫助。 此切換作業可能包括重新格式化磁碟機以及重新安裝作業系統。  
  
### <a name="restore-from-backup"></a>還原備份  
 如果問題與硬體無關，而且確定有未受影響的備份可以使用，請利用該備份來還原資料庫。  
  
 請考慮將資料庫變更為使用 PAGE_VERIFY CHECKSUM 選項。 如需 PAGE_VERIFY 的資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [管理 suspect_pages 資料表 &#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
