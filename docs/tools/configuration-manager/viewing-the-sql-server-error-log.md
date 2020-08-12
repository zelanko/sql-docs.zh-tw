---
title: 檢視 SQL Server 錯誤記錄
description: 檢視目前錯誤記錄檔或先前記錄檔的備份，藉以取得偵測 SQL Server 問題的協助，以檢查進程是否順利完成。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: eb601b3d336a69effc17829a3e9445f06a3857c4
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880271"
---
# <a name="viewing-the-sql-server-error-log"></a>檢視 SQL Server 錯誤記錄
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  您可以檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，確定處理序已順利完成 (例如，備份與還原作業、批次命令或其他指令碼和處理序)。 這有助於偵測任何目前的或潛在的問題區域，包括自動復原訊息 (尤其是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體已停止又重新啟動時)、核心訊息或其他伺服器層級的錯誤訊息。  
  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或任何文字編輯器來檢視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 錯誤記錄檔。 如需有關如何檢視錯誤記錄檔的詳細資訊，請參閱＜ [Open Log File Viewer](../../relational-databases/logs/open-log-file-viewer.md)＞。 根據預設，錯誤記錄檔是位於 `Program Files\Microsoft SQL Server\MSSQL.`*n*`\MSSQL\LOG\ERRORLOG` 和 `ERRORLOG.`*n* 檔案中。  
  
 每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，就會建立新的錯誤記錄檔，不過， [sp_cycle_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md) 系統預存程序可用來循環錯誤記錄檔，而不必重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 通常， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保留前 6 個記錄檔的備份，並提供副檔名 .1 給最新的記錄檔備份，提供副檔名 .2 給第二新的備份...依此類推。 目前的錯誤記錄檔並沒有副檔名。  
  
 請注意，您也可以在離線或無法啟動的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔。 如需詳細資訊，請參閱 [檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)。  
  
  
