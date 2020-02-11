---
title: MSSQLSERVER_7987 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7987 (Database Engine error)
ms.assetid: 314aebf1-6cdf-488d-a274-ce967fadb57b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0541f066c653a233508a48d7b8f02504d36f25b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62913273"
---
# <a name="mssqlserver_7987"></a>MSSQLSERVER_7987
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|7987|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC2_PRE_CHECKS_CHAIN_LINKAGE_MISMATCH|  
|訊息文字|系統資料表預先檢查: 物件識別碼 O_ID 鏈結不相符。 P_ID1->下一頁 = P_ID2，但 P_ID2->上一頁 = P_ID3。 由於無法修復的錯誤，檢查陳述式已經結束。|  
  
## <a name="explanation"></a>說明  
 DBCC CHECKDB 的第一階段是針對關鍵的系統資料表，執行資料頁的基本檢查。 如果找到任何錯誤，由於無法修復錯誤，因此 DBCC CHECKDB 會立即結束。  
  
 *P_ID1* 頁面的下一頁指標指向 *P_ID2* 頁面；但是 *P_ID2* 頁面的上一頁指標卻指向 *P_ID3* 頁面，而未正確地往回指向 *P_ID1* 頁面。  
  
## <a name="user-action"></a>使用者動作  
  
### <a name="look-for-hardware-failure"></a>尋找硬體故障  
 請執行硬體診斷並更正所有問題， 同時檢查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 系統和應用程式記錄檔以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，以查看錯誤發生的原因是否為硬體故障。 請修正前述記錄檔中所包含的任何硬體相關問題。  
  
 若有持續發生的資料損毀問題，請嘗試抽換不同的硬體元件以隔離問題。 請檢查以確認系統並未啟用磁碟控制器上的寫入快取功能。 如果您懷疑寫入快取就是問題所在，請與您的硬體廠商連絡。  
  
 最後，切換到新的硬體系統可能也會有幫助。 此切換作業可能包括重新格式化磁碟機以及重新安裝作業系統。  
  
### <a name="restore-from-backup"></a>還原備份  
 如果問題與硬體無關，而且確定有未受影響的備份可以使用，請利用該備份來還原資料庫。  
  
### <a name="run-dbcc-checkdb"></a>執行 DBCC CHECKDB  
 不適用。 此錯誤無法自動修復。 如果無法從備份還原資料庫，請連絡 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 服務及支援中心 (CSS)。  
  
  
