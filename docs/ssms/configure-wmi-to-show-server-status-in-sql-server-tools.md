---
title: "設定 WMI 以在 SQL Server 工具中顯示伺服器狀態 | Microsoft Docs"
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
- WMI Provider for Server Events, setting permissions
- WMI permissions [SQL Server]
ms.assetid: 7e97197b-ed4d-40d1-9a52-9ab1d92401d7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 950c4d2fdef0359042ebbed168c761e44316ab03
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="configure-wmi-to-show-server-status-in-sql-server-tools"></a>設定 WMI 在 SQL Server 工具中顯示伺服器狀態
此主題描述如何在 [!INCLUDE[ssCurrent](../includes/sscurrent_md.md)] 中設定 WMI，以在 SQL Server 工具中顯示伺服器狀態。 連接到伺服器時， [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]的 [已註冊的伺服器] 和 [物件總管] 元件，以及「 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 組態管理員」，都會使用 Windows Management Instrumentation (WMI) 來取得 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] (MSSQLSERVER) 及 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] Agent (MSSQLSERVER) 服務的狀態。 若要顯示這些服務的狀態，使用者必須具有從遠端存取 WMI 物件的權限。 伺服器必須安裝 WMI，才能設定此權限。  
  
## <a name="SSMSProcedure"></a>若要設定 WMI 權限  
  
1.  在遠端伺服器的 [開始] 功能表上按一下 [執行]。  
  
2.  在 [開啟] 方塊中輸入 **wmimgmt.msc**，再按 [確定]。  
  
3.  在 **Windows Management Infrastructure** 程式中，以滑鼠右鍵按一下 [WMI 控制 (本機)]，然後按一下[內容]。  
  
4.  在 [WMI 控制 (本機) 內容] 對話方塊的 [安全性] 索引標籤上，展開 [Root]，然後按一下 [CIMV2]。  
  
5.  按一下 [安全性] 以開啟 [安全性 ROOT\CIMV2] 對話方塊。  
  
6.  新增群組或使用者至 [群組或使用者名稱] 方塊，然後選取此新增項目。  
  
7.  在 [*<group or user>* 的權限] 方塊中，針對想要遠端偵測其服務狀態的使用者，選取 [遠端啟用] 權限的 [允許] 資料行。  
  
## <a name="see-also"></a>另請參閱  
[啟動、停止或暫停 SQL Server Agent 服務](../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  

