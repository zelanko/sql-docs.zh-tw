---
title: 查看 Integration Services 服務的事件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- events [Integration Services]
- service [Integration Services], events
- Integration Services service, events
ms.assetid: 37e23946-10d1-4116-8568-8fd24067102e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4be91309e4feb34bd8dfd85aee8e3e0cd1f82ffd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054667"
---
# <a name="view-events-for-the-integration-services-service"></a>檢視 Integration Services 服務的事件
  目前有兩個工具可讓您用來檢視 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務的事件：  
  
-   **中的** [記錄檔檢視器] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]對話方塊。 **[記錄檔檢視器]** 對話方塊包括匯出、篩選和搜尋記錄檔的選項。 如需 [記錄檔檢視器][**中選項的詳細資訊，請參閱**記錄檔檢視器 F1 說明](../relational-databases/logs/log-file-viewer-f1-help.md)。  
  
-   Windows 事件檢視器。  
  
 如需 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務所記錄之事件的描述，請參閱 [Integration Services 服務所記錄的事件](service/events-logged-by-the-integration-services-service.md)。  
  
### <a name="to-view-service-events-for-integration-services-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中檢視 Integration Services 的服務事件  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  在 **[檔案]** 功能表上，按一下 **[連接物件總管]**。  
  
3.  在 **[連接到伺服器]** 對話方塊中，選取 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器類型，選取或尋找要連接的伺服器，然後按一下 **[連接]**。  
  
4.  在物件總管中，以滑鼠右鍵按一下 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]，然後按一下 [檢視記錄]****。  
  
5.  若要檢視 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 事件，請選取 **[SQL Server Integration Services]**。 **[NT 事件]** 選項會隨 **[SQL Server Integration Services]** 選項的選取和清除而自動選取和清除。  
  
### <a name="to-view-service-events-for-integration-services-in-windows-event-viewer"></a>在 Windows 事件檢視器中檢視 Integration Services 的服務事件  
  
1.  在 **[控制台]** 中，如果您使用「一般檢視」，請按一下 **[系統管理工具]**，如果您使用「類別檢視」，請按一下 **[效能及維護]** ，然後按一下 **[系統管理工具]**。  
  
2.  按一下 **[事件檢視器]**。  
  
3.  在 **[事件檢視器]** 對話方塊中，按一下 **[應用程式]**。  
  
4.  在 [應用程式]**** 嵌入式管理單元中，尋找 [來源]**** 資料行中值為 **SQLISService** 的項目，以滑鼠右鍵按一下該項目，然後按一下 [屬性]****。  
  
5.  選擇性地按一下向上箭頭或向下箭頭，以顯示上一個或下一個事件。  
  
6.  選擇性地按一下 [複製至剪貼簿] 圖示，以複製事件資訊。  
  
7.  選擇使用位元組或文字顯示事件資料。  
  
8.  按一下 [確定]  。  
  
9. 在 **[檔案]** 功能表上，按一下 **[結束]** ，以關閉 **[事件檢視器]** 對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Integration Services 服務](../../2014/integration-services/manage-the-integration-services-service.md)   
 [加入資料流程效能計數器的記錄檔](performance/performance-counters.md)  
  
  
