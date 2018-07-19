---
title: MSSQLSERVER_7988 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7988 (Database Engine error)
ms.assetid: 29b967b8-de30-4618-99a8-8b1155e69026
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 594af53f01ad379da27cdacccaf3802eea1fb620
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34326279"
---
# <a name="mssqlserver7988"></a>MSSQLSERVER_7988
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|7988|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC2_PRE_CHECKS_CHAIN_LOOP_DETECTED|  
|訊息文字|統資料表預先檢查: 物件識別碼 O_ID。 於 P_ID 偵測到資料鍊迴圈。 由於無法修復的錯誤，檢查陳述式已經結束。|  
  
## <a name="explanation"></a>說明  
DBCC CHECKDB 的第一階段是針對關鍵的系統資料表，執行資料頁的基本檢查。 如果找到任何錯誤，由於無法修復錯誤，因此 DBCC CHECKDB 會立即結束。 已經在頁面 *P_ID* 上偵測到頁面連結迴圈。 若某個頁面的下一頁指標最後會返回該頁面，便會發生頁面連結迴圈。  
  
## <a name="user-action"></a>使用者動作  
  
### <a name="look-for-hardware-failure"></a>尋找硬體故障  
請執行硬體診斷並更正所有問題， 同時檢查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 系統和應用程式記錄檔以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，以查看錯誤發生的原因是否為硬體故障。 請修正前述記錄檔中所包含的任何硬體相關問題。  
  
若有持續發生的資料損毀問題，請嘗試抽換不同的硬體元件以隔離問題。 請檢查以確認系統並未啟用磁碟控制器上的寫入快取功能。 如果您懷疑寫入快取就是問題所在，請與您的硬體廠商連絡。  
  
最後，切換到新的硬體系統可能也會有幫助。 此切換作業可能包括重新格式化磁碟機以及重新安裝作業系統。  
  
### <a name="restore-from-backup"></a>還原備份  
如果問題與硬體無關，而且確定有未受影響的備份可以使用，請利用該備份來還原資料庫。  
  
### <a name="run-dbcc-checkdb"></a>執行 DBCC CHECKDB  
不適用。 此錯誤無法自動修復。 如果無法從備份還原資料庫，請連絡 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 服務及支援中心 (CSS)。  
  
