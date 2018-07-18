---
title: 記錄檔檢視器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Log File Viewer
ms.assetid: a4ea7fc8-1cb2-4c98-bc86-8991c5e748b2
caps.latest.revision: 26
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 44f5ed33bef9ff57e6bc0c4262a950069ec5b480
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32942143"
---
# <a name="log-file-viewer"></a>記錄檔檢視器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的記錄檔檢視器是用於存取有關記錄檔中所擷取之錯誤和事件的資訊。  
  
## <a name="benefits-of-using-log-file-viewer"></a>記錄檔檢視器的優點  
 當目標執行個體已離線或無法啟動時，您可以從本機或遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄檔。 您可以從 [已註冊的伺服器] 存取離線記錄檔，也可以透過 WMI 和 WQL (WMI 查詢語言) 查詢以程式設計方式存取。 如需詳細資訊，請參閱 [檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)。 下列是您可以使用記錄檔檢視器存取的記錄檔類型：  
  
-   稽核集合  
  
-   資料收集  
  
-   Database Mail  
  
-   作業記錄  
  
-   維護計畫  
  
-   遠端維護計畫  
  
-   [SQL Server]  
  
-   SQL Server Agent  
  
-   Windows NT (這些是也可以從事件檢視器存取的 Windows 事件)。  
  
## <a name="log-file-viewer-tasks"></a>記錄檔檢視器工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何根據想要檢視的資訊來開啟記錄檔檢視器。|[開啟記錄檔檢視器](../../relational-databases/logs/open-log-file-viewer.md)|  
|描述如何透過已註冊的伺服器來檢視離線記錄檔，以及如何驗證 WMI 權限。|[檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)|  
|提供記錄檔檢視器 F1 説明。|[記錄檔檢視器 F1 說明](../../relational-databases/logs/log-file-viewer-f1-help.md)|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [SQL Server Agent 錯誤記錄檔](http://msdn.microsoft.com/library/0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41)  
  
  
