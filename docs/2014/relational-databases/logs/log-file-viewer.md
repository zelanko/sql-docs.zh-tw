---
title: 記錄檔檢視器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Log File Viewer
ms.assetid: a4ea7fc8-1cb2-4c98-bc86-8991c5e748b2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3cc7a4fd33dba71723a353d8ca3cb0d3f9e21e9b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85024712"
---
# <a name="log-file-viewer"></a>記錄檔檢視器
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的記錄檔檢視器是用於存取有關記錄檔中所擷取之錯誤和事件的資訊。  
  
## <a name="benefits-of-using-log-file-viewer"></a>記錄檔檢視器的優點  
 當目標執行個體已離線或無法啟動時，您可以從本機或遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄檔。 您可以從 [已註冊的伺服器] 存取離線記錄檔，也可以透過 WMI 和 WQL (WMI 查詢語言) 查詢以程式設計方式存取。 如需詳細資訊，請參閱 [檢視離線記錄檔](view-offline-log-files.md)。 下列是您可以使用記錄檔檢視器存取的記錄檔類型：  
  
-   稽核集合  
  
-   資料收集  
  
-   Database Mail  
  
-   作業記錄  
  
-   維護計畫  
  
-   遠端維護計畫  
  
-   SQL Server  
  
-   SQL Server Agent  
  
-   Windows NT (這些是也可以從事件檢視器存取的 Windows 事件)。  
  
## <a name="log-file-viewer-tasks"></a>記錄檔檢視器工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何根據想要檢視的資訊來開啟記錄檔檢視器。|[開啟記錄檔檢視器](open-log-file-viewer.md)|  
|描述如何透過已註冊的伺服器來檢視離線記錄檔，以及如何驗證 WMI 權限。|[檢視離線記錄檔](view-offline-log-files.md)|  
|提供記錄檔檢視器 F1 説明。|[記錄檔檢視器 F1 說明](log-file-viewer-f1-help.md)|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Audit &#40;Database Engine&#41;](../security/auditing/sql-server-audit-database-engine.md)   
 [SQL Server Agent 錯誤記錄檔](../../ssms/agent/sql-server-agent-error-log.md)  
  
  
