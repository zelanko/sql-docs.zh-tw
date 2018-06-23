---
title: 將設定的 SQL Server 執行個體自動啟動 （SQL Server 組態管理員） |Microsoft 文件
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
caps.latest.revision: 34
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4b34f2831a39de5dea2353a6114f2ae36388bd7f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035052"
---
# <a name="set-an-instance-of-sql-server-to-start-automatically-sql-server-configuration-manager"></a>將 SQL Server 執行個體設定為自動啟動 (SQL Server 組態管理員)
  此主題描述如何使用 SQL Server 組態管理員，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中設定 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體自動啟動。 在安裝期間， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通常會設定為自動啟動。 如果沒有這樣執行，您隨時都可以變更該設定。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>將 SQL Server 執行個體設定為自動啟動  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]**，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
    > [!NOTE]  
    >  由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 程式的嵌入式管理單元，而不是獨立的程式，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員在較新版本的 Windows 中不會作為應用程式出現。  
    >   
    >  -   **Windows 10**：  
    >          若要開啟[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager 上**起始頁**，輸入 SQLServerManager12.msc (如[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])。 針對先前版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以較小的數字取代 12。 按一下 SQLServerManager12.msc 會開啟 Configuration Manager。 組態管理員釘選到起始頁或工作列，SQLServerManager12.msc，以滑鼠右鍵按一下，然後按一下**開啟檔案位置**。 在 [Windows 檔案總管] 中，SQLServerManager12.msc，以滑鼠右鍵按一下，然後按一下**釘選到開始**或**釘選到工作列**。  
    > -   **Windows 8**：  
    >          若要開啟[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager，請在**搜尋**快速鍵**應用程式**，型別**Sqlservermanager<\<版本 >.msc**例如`SQLServerManager12.msc`，然後按下**Enter**。  
  
2.  在 **[SQL Server 組態管理員]** 中展開 **[服務]**，然後按一下 **[SQL Server]**。  
  
3.  在詳細資料窗格中，以滑鼠右鍵按一下您想要自動啟動的執行個體名稱，然後按一下 [屬性]。  
  
4.  在 [SQL Server \<執行個體名稱> 屬性]**** 對話方塊中，將 [啟動模式] 設定為 [自動]。  
  
5.  按一下 **[確定]**，然後關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
## <a name="see-also"></a>另請參閱  
 [避免自動啟動 SQL Server 的執行個體 &#40;SQL Server 組態管理員&#41;](scm-services-prevent-automatic-startup-of-an-instance.md)   
 [連接至另一部電腦 &#40;SQL Server 組態管理員&#41;](scm-services-connect-to-another-computer.md)   
 [設定 WMI 在 SQL Server 工具中顯示伺服器狀態](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  