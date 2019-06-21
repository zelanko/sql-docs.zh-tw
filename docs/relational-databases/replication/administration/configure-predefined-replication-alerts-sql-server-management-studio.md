---
title: 設定預先定義的複寫警示 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b90293de93fd032f7ebc1ee77d839cc2211a7e9d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63051749"
---
# <a name="configure-predefined-replication-alerts-sql-server-management-studio"></a>設定預先定義的複寫警示 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  複寫提供下列預先定義的警示，這些警示可設定為回應複寫事件：  
  
-   **複寫: 代理程式成功**  
  
-   **複寫: 代理程式失敗**  
  
-   **複寫: 代理程式重試**  
  
-   **複寫: 已卸除逾期的訂閱**  
  
-   **複寫：驗證失敗後重新初始化訂閱**  
  
-   **複寫：訂閱者資料驗證失敗**  
  
-   **複寫：訂閱者已經通過資料驗證**  
  
-   **複寫: 代理程式自訂關閉**  
  
 在  中的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] or the **Warnings** tab in Replication Monitor. 如需有關存取此索引標籤的詳細資訊，請參閱[使用複寫監視器來檢視資訊及執行工作](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
 除了這些警示外，複寫監視器還提供與狀態和效能相關的警告與警示集合。 如需相關資訊，請參閱 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。 您也可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 警示基礎結構，為其他複寫事件定義警示。 如需詳細資訊，請參閱[建立使用者定義的事件](https://msdn.microsoft.com/library/03d71a35-97fa-4bba-aa9a-23ac9c9cf879)。  
  
### <a name="to-configure-a-predefined-replication-alert-in-management-studio"></a>若要在 Management Studio 中設定預先定義的複寫警示  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的散發者，然後展開伺服器節點。  
  
2.  展開 **[SQL Server Agent]** 資料夾，然後展開 **[警示]** 資料夾。  
  
3.  以滑鼠右鍵按一下複寫警示，然後按一下 **[屬性]** 。  
  
4.  在 [\<警示名稱> 警示屬性]  對話方塊中設定選項：  
  
    -   在 **[一般]** 頁面上，按一下 **[啟用]** ；指定警示應套用至哪個資料庫。  
  
    -   在 **[回應]** 頁面上，指定是否應傳送電子郵件及 (或) 是否應執行作業。  
  
         若警示是**複寫：** 訂閱者資料驗證失敗」，您可以指定複寫為此警示提供的回應作業：選取 [執行作業]  ，然後按一下瀏覽按鈕 ( **…** )。 在 **[尋找作業]** 對話方塊中，按一下 **[瀏覽]** 。 在 **[瀏覽物件]** 對話方塊中，選取 **[重新初始化具有資料驗證失敗的訂閱]** 。 在兩個開啟的對話方塊中按一下 **[確定]** 。 執行作業時，它會使用對預存程序的遠端程序呼叫 (RPC) 重新初始化訂閱。 如果「發行者」使用遠端「散發者」，則必須定義「發行者」端的遠端伺服器登入，以便建立從「散發者」到「發行者」的 RPC。  
  
    -   在 **[選項]** 頁面上，自訂回應的文字。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-configure-an-alert-for-a-threshold-in-replication-monitor"></a>若要在複寫監視器中設定臨界值的警示  
  
1.  在 **[警告]** 索引標籤上，按一下 **[設定警示]** 。  
  
2.  在 **[設定複寫警示]** 對話方塊中選取一個警示，然後按一下 **[設定]** 。  
  
3.  在 [\<警示名稱> 警示屬性]  對話方塊中設定選項：  
  
    -   在 **[一般]** 頁面上，按一下 **[啟用]** ；指定警示應套用至哪個資料庫。  
  
    -   在 **[回應]** 頁面上，指定是否應傳送電子郵件及 (或) 是否應執行作業。  
  
         若警示是**複寫：** 訂閱者資料驗證失敗」，您可以指定複寫為此警示提供的回應作業：選取 [執行作業]  ，然後按一下瀏覽按鈕 ( **…** )。 在 **[尋找作業]** 對話方塊中，按一下 **[瀏覽]** 。 在 **[瀏覽物件]** 對話方塊中，選取 **[重新初始化具有資料驗證失敗的訂閱]** 。 在兩個開啟的對話方塊中按一下 **[確定]** 。 執行作業時，它會使用對預存程序的遠端程序呼叫 (RPC) 重新初始化訂閱。 如果「發行者」使用遠端「散發者」，則必須定義「發行者」端的遠端伺服器登入，以便建立從「散發者」到「發行者」的 RPC。  
  
    -   在 **[選項]** 頁面上，自訂回應的文字。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  按一下 [ **關閉**]。  
  
## <a name="see-also"></a>另請參閱  
 [使用複寫代理程式事件的警示](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)  
  
  
