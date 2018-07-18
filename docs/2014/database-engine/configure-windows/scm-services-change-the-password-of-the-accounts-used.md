---
title: 變更 SQL Server （SQL Server 組態管理員） 所使用之帳戶的密碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- expired password [SQL Server], SQL Server Agent
- passwords [SQL Server], SQL Server Agent service
- passwords [SQL Server], changing
- expired password [SQL Server], Database Engine
- passwords [SQL Server], SQL Server service
- Database Engine [SQL Server], passwords
- changing passwords used by SQL Server
- modifying passwords
ms.assetid: 5b6dcc03-6cae-45d3-acef-6f85ca6d615f
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 37e989b7849cf3d3168df81b51733a49beaa8915
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37207568"
---
# <a name="change-the-password-of-the-accounts-used-by-sql-server-sql-server-configuration-manager"></a>變更 SQL Server 所使用之帳戶的密碼 (SQL Server 組態管理員)
  此主題描述如何使用 SQL Server 組態管理員，在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Agent 所使用之帳戶的密碼。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會使用安裝過程中最初提供的認證，在電腦上當做服務執行。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體在網域帳戶下執行，而且該帳戶的密碼已變更時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所使用的密碼就必須更新為新的密碼。 如果沒有更新密碼， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會喪失某些網域資源的存取權，而且如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 停止，服務就要等到密碼更新後才會重新啟動。  
  
 若要變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼，請參閱 [密碼已過期](../password-expired.md)。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是已獲授權專供變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務各項設定而設計的工具。 使用 Windows 服務控制管理員 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] services.msc **) 應用程式變更**服務時，不一定能變更所有必要的設定，而且可能導致服務無法正常運作。 不過，在叢集環境的使用中節點上透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員變更密碼之後，必須在被動節點上使用服務控制管理員變更密碼。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須是電腦的系統管理員才能變更服務所使用的密碼。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-change-the-password-used-by-the-sql-server-database-engine-service"></a>變更 SQL Server Agent (Database Engine) 服務所使用的密碼  
  
1.  按一下 **[開始]** 按鈕，然後依序指向 **[所有程式]**、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
    > [!NOTE]  
    >  因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理主控台程式的嵌入式管理單元，而不是獨立的程式，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員在較新版本的 Windows 中不會作為應用程式出現。  
    >   
    >  -   **Windows 10**：  
    >          若要開啟  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager，請在**起始頁**，輸入 SQLServerManager12.msc (如[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])。 針對先前版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以較小的數字取代 12。 按一下 SQLServerManager12.msc 開啟 Configuration Manager。 組態管理員釘選到起始頁或工作列，SQLServerManager12.msc，以滑鼠右鍵按一下，然後按一下**開啟檔案位置**。 在 Windows 檔案總管 中，SQLServerManager12.msc，以滑鼠右鍵按一下，然後按一下**釘選到開始**或是**釘選到工作列**。  
    > -   **Windows 8**：  
    >          若要開啟  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager，請在**搜尋**快速鍵**應用程式**，型別**SQLServerManager\<版本 >.msc**例如`SQLServerManager12.msc`，然後按下**Enter**。  
  
2.  在 [SQL Server 組態管理員] 中，按一下 **[SQL Server 服務]**。  
  
3.  在詳細資料窗格中，以滑鼠右鍵按一下 [SQL Server (\<執行個體名稱>)]，然後按一下 [屬性]。  
  
4.  在 [SQL Server (\<執行個體名稱>) 屬性] 對話方塊的 [登入] 索引標籤上，針對列於 [帳戶名稱] 方塊的帳戶，在 [密碼] 和 [確認密碼] 方塊中鍵入新密碼，然後按一下 [確定]。  
  
     密碼會立即生效，不需重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
#### <a name="to-change-the-password-used-by-the-sql-server-agent-service"></a>變更 SQL Server Agent 服務所使用的密碼  
  
1.  按一下 **[開始]** 按鈕，然後依序指向 **[所有程式]**、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
2.  在 [SQL Server 組態管理員] 中，按一下 **[SQL Server 服務]**。  
  
3.  在詳細資料窗格中，以滑鼠右鍵按一下 [SQL Server Agent (\<執行個體名稱>)]，然後按一下 [屬性]。  
  
4.  在 [SQL Server Agent (\<執行個體名稱>) 屬性] 對話方塊的 [登入] 索引標籤上，針對列於 [帳戶名稱] 方塊的帳戶，在 [密碼] 和 [確認密碼] 方塊中鍵入新密碼，然後按一下 [確定]。  
  
     在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]獨立執行個體上，密碼會立即生效，不需要重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在叢集執行個體上， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源離線，而且需要重新啟動。  
  
## <a name="see-also"></a>另請參閱  
 [管理服務的如何主題 &#40;SQL Server 組態管理員&#41;](../managing-services-how-to-topics-sql-server-configuration-manager.md)  
  
  
