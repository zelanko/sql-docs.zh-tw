---
title: MSSQLSERVER_3159 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3159 (Database Engine error)
ms.assetid: c93c1003-0e3a-40aa-9873-44a0f5b8b57e
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c56353d445e362e13811e377449efde26695a57b
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver3159"></a>MSSQLSERVER_3159
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|3159|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LDDB_LOGNOTBACKEDUP|  
|訊息文字|資料庫 "%ls" 的記錄結尾尚未備份。 若您不想遺失其中的內容，請使用 BACKUP LOG WITH NORECOVERY 備份記錄。 亦可使用 RESTORE 陳述式的 WITH REPLACE 或 WITH STOPAT 子句，覆寫記錄的內容。|  
  
## <a name="explanation"></a>說明  
在完整或大量記錄復原模式下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 多半會要求您備份記錄的結尾，以便擷取尚未備份的記錄。 在還原作業之前對記錄結尾進行的記錄備份，就稱為「結尾記錄備份」。  
  
當您將資料庫復原到失敗點時，結尾記錄備份是復原計畫中重要的最後備份。 如果您無法備份記錄的結尾，則只能將資料庫復原到失敗前建立的最後一個備份的結尾。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通常會要求您在開始還原資料庫之前進行結尾記錄備份。 結尾記錄備份可防止工作遺失，並保持記錄鏈結完整。 但是，並非所有的還原狀況都需要結尾記錄備份。 如果復原點已包含在較早的記錄備份中，或者您要移動或取代 (覆寫) 資料庫，就不需要有結尾記錄備份，而且不需要將它還原至最近備份之後的某個時間點。 此外，如果記錄檔損毀，而且無法建立結尾記錄備份，您也必須在不使用結尾記錄備份的情況下還原資料庫。 任何在最近一次記錄備份之後認可的交易都會遺失。 如需詳細資訊，請參閱本主題稍後的「不使用結尾記錄備份而進行還原」。  
  
> [!CAUTION]  
> REPLACE 不應經常使用，而且只應在審慎考量之後使用。  
  
## <a name="user-action"></a>使用者動作  
進行結尾記錄備份，接著再重試一次還原作業。  
  
如果無法備份記錄結尾，請在 RESTORE 陳述式中使用 WITH STOPAT 或 WITH REPLACE。  
  
## <a name="see-also"></a>另請參閱  
[將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](~/relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
[資料庫損毀時備份交易記錄 &#40;SQL Server&#41;](~/relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
[備份交易記錄 &#40;SQL Server&#41;](~/relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
[結尾記錄備份 &#40;SQL Server&#41;](~/relational-databases/backup-restore/tail-log-backups-sql-server.md)  
  
