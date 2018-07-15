---
title: 監視錯誤記錄檔 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server]
- database performance [SQL Server], errors
- Windows application logs [SQL Server]
- monitoring performance [SQL Server], errors
- server performance [SQL Server], errors
- comparing error and application log output
- errors [SQL Server], logs
- tuning databases [SQL Server], errors
- database monitoring [SQL Server], errors
- SQL Server error log
- logs [SQL Server], SQL Server error logs
- error logs [SQL Server]
- logs [SQL Server], Windows application logs
ms.assetid: e250336b-0695-44f6-a42f-23222f94e377
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b57393f61c0acdb39adec511f31dec8f5b266de
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200588"
---
# <a name="monitoring-the-error-logs"></a>監視錯誤記錄
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將特定系統事件和使用者自訂事件記錄到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄檔中。 這兩種記錄檔都會自動替所有記錄的事件加入時間戳記。 請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中的資訊來解決 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的相關問題。  
  
 Windows 應用程式記錄檔可針對 Windows 作業系統上所發生的事件，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 中的事件，提供整體描述。 使用「Windows 事件檢視器」可檢視 Windows 應用程式記錄檔，以及篩選資訊。 例如，您可以篩選事件，例如資訊、警告、錯誤、成功稽核與失敗稽核。  
  
## <a name="comparing-error-and-application-log-output"></a>比較錯誤與應用程式記錄輸出  
 您可以同時使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔和 Windows 應用程式記錄檔，來找出問題的原因。 例如，在監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔時，您可能會收到不含原因資訊的錯誤訊息。 藉由比較這些記錄之間的事件日期和時間，可以縮小可能原因的範圍。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 記錄檔檢視器可讓您將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 與 Windows 記錄檔整合為一份清單，以便輕鬆地了解相關的伺服器事件與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜記錄檔檢視器＞主題。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[檢視 SQL Server 錯誤記錄檔](../../../2014/tools/configuration-manager/viewing-the-sql-server-error-log.md)|包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔及其檢視方式的詳細資訊。|  
|[檢視 Windows 應用程式記錄檔](viewing-the-windows-application-log.md)|包含 Windows 應用程式記錄檔及其檢視方式的詳細資訊。|  
  
  
