---
title: "設定登入稽核 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], logins
- logins [SQL Server], auditing
ms.assetid: 16961116-57ac-4eef-8037-791b26ade548
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1153704ae4f345436c05a37cae98a522ef991ba1
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="configure-login-auditing-sql-server-management-studio"></a>設定登入稽核 (SQL Server Management Studio)
此主題描述如何在 [!INCLUDE[ssCurrent](../includes/sscurrent_md.md)] 中設定登入稽核，以監視 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion_md.md)] 登入活動。 可設定登入稽核，針對以下事件寫入錯誤記錄檔。  
  
-   失敗的登入  
  
-   成功的登入  
  
-   失敗和成功的登入  
  
您必須重新啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] ，這個選項才會生效。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-configure-login-auditing"></a>若要設定登入稽核  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 中，使用 [物件總管] 連接到 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion_md.md)] 的執行個體。  
  
2.  在物件總管中，以滑鼠右鍵按一下伺服器名稱，然後按一下 [屬性]。  
  
3.  在 [安全性] 頁面的 [登入稽核] 底下，按一下所需的選項並關閉 [伺服器屬性] 頁面。  
  
4.  在物件總管中，以滑鼠右鍵按一下伺服器名稱，然後按一下 [重新啟動]。  
  

