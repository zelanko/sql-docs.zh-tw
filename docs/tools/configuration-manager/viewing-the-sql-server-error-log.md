---
title: "檢視 SQL Server 錯誤記錄 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "循環 SQL Server 錯誤記錄"
  - "檢視 SQL Server 錯誤記錄"
  - "錯誤 [SQL Server], 記錄檔"
  - "SQL Server 錯誤記錄"
  - "顯示 SQL Server 錯誤記錄"
  - "記錄 [SQL Server], SQL Server 錯誤記錄檔"
ms.assetid: 6908c21a-65e3-458f-a272-fee256d86448
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 檢視 SQL Server 錯誤記錄
  您可以檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，確定處理序已順利完成 (例如，備份與還原作業、批次命令或其他指令碼和處理序)。 這有助於偵測任何目前的或潛在的問題區域，包括自動復原訊息 (尤其是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體已停止又重新啟動時)、核心訊息或其他伺服器層級的錯誤訊息。  
  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或任何文字編輯器來檢視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 錯誤記錄檔。 如需有關如何檢視錯誤記錄檔的詳細資訊，請參閱＜ [Open Log File Viewer](../../relational-databases/logs/open-log-file-viewer.md)＞。 根據預設，錯誤記錄檔是位於 `Program Files\Microsoft SQL Server\MSSQL.`*n*`\MSSQL\LOG\ERRORLOG` 和 `ERRORLOG.`*n* 檔案中。  
  
 每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，就會建立新的錯誤記錄檔，不過，[sp_cycle_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md) 系統預存程序可用來循環錯誤記錄檔，而不必重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 通常， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保留前 6 個記錄檔的備份，並提供副檔名 .1 給最新的記錄檔備份，提供副檔名 .2 給第二新的備份...依此類推。 目前的錯誤記錄檔並沒有副檔名。  
  
 請注意，您也可以在離線或無法啟動的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔。 如需詳細資訊，請參閱[檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)。  
  
  