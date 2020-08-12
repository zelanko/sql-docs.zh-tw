---
title: 監視錯誤記錄
description: 使用 SQL Server 錯誤記錄檔、Windows 應用程式記錄檔和 SQL Server Management Studio 記錄檔檢視器，針對與 SQL Server 相關的問題進行疑難排解。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
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
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 949a7c358d68ac66104140bb37d443af8b4b4b0f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85894840"
---
# <a name="monitoring-the-error-logs"></a>監視錯誤記錄
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將特定系統事件和使用者自訂事件記錄到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄檔中。 這兩種記錄檔都會自動替所有記錄的事件加入時間戳記。 請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中的資訊來解決 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的相關問題。  
  
 Windows 應用程式記錄檔可針對 Windows 作業系統上所發生的事件，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 中的事件，提供整體描述。 使用「Windows 事件檢視器」可檢視 Windows 應用程式記錄檔，以及篩選資訊。 例如，您可以篩選事件，例如資訊、警告、錯誤、成功稽核與失敗稽核。  
  
## <a name="comparing-error-and-application-log-output"></a>比較錯誤與應用程式記錄輸出  
 您可以同時使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔和 Windows 應用程式記錄檔，來找出問題的原因。 例如，在監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔時，您可能會收到不含原因資訊的錯誤訊息。 藉由比較這些記錄之間的事件日期和時間，可以縮小可能原因的範圍。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 記錄檔檢視器可讓您將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 與 Windows 記錄檔整合為一份清單，以便輕鬆地了解相關的伺服器事件與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜記錄檔檢視器＞主題。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|說明|  
|-----------|-----------------|  
|[檢視 SQL Server 錯誤記錄檔](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)|包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔及其檢視方式的詳細資訊。|  
|[檢視 Windows 應用程式記錄檔](../../tools/configuration-manager/viewing-the-windows-application-log.md)|包含 Windows 應用程式記錄檔及其檢視方式的詳細資訊。|  
  
  
