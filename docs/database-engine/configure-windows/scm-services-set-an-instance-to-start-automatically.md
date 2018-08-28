---
title: SCM 服務 - 將執行個體設定為自動啟動 | Microsoft Docs
ms.custom: ''
ms.date: 01/06/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
caps.latest.revision: 35
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 34430bf70af547a54402c776b05ac6666bee8b71
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40412585"
---
# <a name="scm-services---set-an-instance-to-start-automatically"></a>SCM 服務 - 將執行個體設定為自動啟動
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 SQL Server 組態管理員，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中設定 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體自動啟動。 在安裝期間， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通常會設定為自動啟動。 如果沒有這樣執行，您隨時都可以變更該設定。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>將 SQL Server 執行個體設定為自動啟動  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]**，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
    > [!NOTE]  
    >  由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 程式的嵌入式管理單元，而不是獨立的程式，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員在較新版本的 Windows 中不會作為應用程式出現。  
    >   
    >  -   **Windows 10**：  
    >          若要開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，請在 **起始頁**上輸入 SQLServerManager13.msc (適用於 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])。 若為舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則以較小的數字取代 13。 按一下 SQLServerManager13.msc 即可開啟組態管理員。 若要將組態管理員釘選到起始頁或工作列，請以滑鼠右鍵按一下 SQLServerManager13.msc，然後按一下 [開啟檔案位置]。 在 Windows 檔案總管中，以滑鼠右鍵按一下 SQLServerManager13.msc，然後按一下 [釘選到 [開始] 功能表] 或 [釘選到工作列]。  
    > -   **Windows 8**：  
    >          若要開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，請在 [搜尋] 常用鍵的 [應用程式] 下，鍵入 **SQLServerManager\<版本>.msc** (例如 **SQLServerManager13.msc**)，然後按 **Enter**。  
  
2.  在 **[SQL Server 組態管理員]** 中展開 **[服務]**，然後按一下 **[SQL Server]**。  
  
3.  在詳細資料窗格中，以滑鼠右鍵按一下您想要自動啟動的執行個體名稱，然後按一下 [屬性]。  
  
4.  在 [SQL Server \<執行個體名稱> 屬性]**** 對話方塊中，將 [啟動模式] 設定為 [自動]。  
  
5.  按一下 **[確定]**，然後關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
## <a name="see-also"></a>另請參閱  
 [避免自動啟動 SQL Server 的執行個體 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)   
 [連接至另一部電腦 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/scm-services-connect-to-another-computer.md)   
 [設定 WMI 在 SQL Server 工具中顯示伺服器狀態](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
