---
title: 檢視 SQL Server 錯誤記錄檔 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cycling SQL Server error log
- viewing SQL Server error log
- errors [SQL Server], logs
- SQL Server error log
- displaying SQL Server error log
- logs [SQL Server], SQL Server error logs
ms.assetid: 6908c21a-65e3-458f-a272-fee256d86448
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 88c5b77b4ac0f2d0f8ed579f2ff32eae8c263610
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150301"
---
# <a name="viewing-the-sql-server-error-log"></a>檢視 SQL Server 錯誤記錄
  您可以檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，確定處理序已順利完成 (例如，備份與還原作業、批次命令或其他指令碼和處理序)。 這有助於偵測任何目前的或潛在的問題區域，包括自動復原訊息 (尤其是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體已停止又重新啟動時)、核心訊息或其他伺服器層級的錯誤訊息。  
  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或任何文字編輯器來檢視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 錯誤記錄檔。 如需有關如何檢視錯誤記錄檔的詳細資訊，請參閱＜ [Open Log File Viewer](../../relational-databases/logs/log-file-viewer.md)＞。 根據預設，錯誤記錄檔是位於 `Program Files\Microsoft SQL Server\MSSQL.`*n*`\MSSQL\LOG\ERRORLOG` 和 `ERRORLOG.`*n* 檔案中。  
  
 每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，就會建立新的錯誤記錄檔，不過， [sp_cycle_errorlog](/sql/relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql) 系統預存程序可用來循環錯誤記錄檔，而不必重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 通常， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保留前 6 個記錄檔的備份，並提供副檔名 .1 給最新的記錄檔備份，提供副檔名 .2 給第二新的備份...依此類推。 目前的錯誤記錄檔並沒有副檔名。  
  
 請注意，您也可以在離線或無法啟動的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔。 如需詳細資訊，請參閱 [檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)。  
  
  
