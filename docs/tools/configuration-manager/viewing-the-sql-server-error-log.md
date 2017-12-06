---
title: "檢視 SQL Server 錯誤記錄檔 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cycling SQL Server error log
- viewing SQL Server error log
- errors [SQL Server], logs
- SQL Server error log
- displaying SQL Server error log
- logs [SQL Server], SQL Server error logs
ms.assetid: 6908c21a-65e3-458f-a272-fee256d86448
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f25d82815803d6003d5b9196c4f38caf012beaeb
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="viewing-the-sql-server-error-log"></a>檢視 SQL Server 錯誤記錄
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]檢視[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]錯誤記錄檔，以確保，處理序已順利完成 （例如備份和還原作業、 批次命令，或其他指令碼和處理程序）。 這有助於偵測任何目前的或潛在的問題區域，包括自動復原訊息 (尤其是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體已停止又重新啟動時)、核心訊息或其他伺服器層級的錯誤訊息。  
  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或任何文字編輯器來檢視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 錯誤記錄檔。 如需有關如何檢視錯誤記錄檔的詳細資訊，請參閱＜ [Open Log File Viewer](../../relational-databases/logs/open-log-file-viewer.md)＞。 根據預設，錯誤記錄檔是位於 `Program Files\Microsoft SQL Server\MSSQL.`*n*`\MSSQL\LOG\ERRORLOG` 和 `ERRORLOG.`*n* 檔案中。  
  
 每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，就會建立新的錯誤記錄檔，不過， [sp_cycle_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md) 系統預存程序可用來循環錯誤記錄檔，而不必重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 通常， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保留前 6 個記錄檔的備份，並提供副檔名 .1 給最新的記錄檔備份，提供副檔名 .2 給第二新的備份...依此類推。 目前的錯誤記錄檔並沒有副檔名。  
  
 請注意，您也可以在離線或無法啟動的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔。 如需詳細資訊，請參閱 [檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)。  
  
  
