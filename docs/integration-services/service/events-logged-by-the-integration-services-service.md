---
title: "Integration Services 服務所記錄的事件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- service [Integration Services], events
- events [Integration Services], service
- Integration Services service, events
ms.assetid: d4122dcf-f16f-47a0-93a2-ffa3d0d4f9cf
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: cc4cd7e190c7cd2ab7fc2bec25505ae8da6f30fe
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="events-logged-by-the-integration-services-service"></a>Integration Services 服務所記錄的事件
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會將各種訊息記錄至 Windows 應用程式事件記錄檔。 當服務啟動、停止以及發生特定問題時，此服務就會記錄這些訊息。  
  
 本主題會提供服務記錄至應用程式事件記錄檔之常見事件訊息的相關資訊。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會記錄這個主題所描述而且事件來源為 SQLISService 的所有訊息。  
  
 如需 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的詳細資訊，請參閱 [Integration Services 服務 &#40;SSIS 服務&#41;](../../integration-services/service/integration-services-service-ssis-service.md)。  
  
## <a name="service-status-messages"></a>服務的狀態訊息
 當您選取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 進行安裝時，系統就會安裝並啟動 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務，而且它的啟動類型會設定為自動。  
  
|事件識別碼|符號名稱|Text|注意|  
|--------------|-------------------|----------|-----------|  
|256|DTS_MSG_SERVER_STARTING|正在啟動 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服務。|服務即將啟動。|  
|257|DTS_MSG_SERVER_STARTED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服務已啟動。|服務已啟動。|  
|260|DTS_MSG_SERVER_START_FAILED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服務無法啟動。%n錯誤: %1|服務無法啟動。 無法啟動的原因可能是安裝已損毀或服務帳戶不正確。|  
|258|DTS_MSG_SERVER_STOPPING|正在停止 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服務。%n%n結束時停止所有執行中的封裝: %1|服務正在停止，而且如果您將此服務設定為這樣做，就會停止所有執行中的封裝。 您可以在組態檔中設定 True 或 False 值，以便決定在此服務本身停止時，是否會停止執行中封裝。 這個事件的訊息包括這項設定的值。|  
|259|DTS_MSG_SERVER_STOPPED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服務已停止。%n伺服器版本 %1|服務已停止。|  
  
## <a name="settings-file-messages"></a>設定檔訊息  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的設定會儲存在您可以修改的 XML 檔案中。 如需詳細資訊，請參閱 [Integration Services Service &#40;SSIS Service&#41;](../../integration-services/service/integration-services-service-ssis-service.md) (Integration Services 服務 (SSIS 服務))。  
  
|이벤트 ID|符號名稱|Text|注意|  
|--------------|-------------------|----------|-----------|  
|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服務: %n指定組態檔的登錄設定不存在。 %n嘗試載入預設組態檔。|包含組態檔路徑的登錄項目不存在或是空的。|  
|272|DTS_MSG_SERVER_MISSING_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服務組態檔不存在。%n載入預設值。|組態檔本身不存在指定的位置中。|  
|273|DTS_MSG_SERVER_BAD_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服務組態檔不正確。%n讀取組態檔時發生錯誤: %1%n%n以預設值來載入伺服器。|組態檔無法讀取或無效。 這個錯誤可能是由於檔案中的 XML 語法錯誤所造成。|  
  
## <a name="other-messages"></a>其他訊息  
  
|事件識別碼|符號名稱|Text|注意|  
|--------------|-------------------|----------|-----------|  
|336|DTS_MSG_SERVER_STOPPING_PACKAGE|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服務: 停止執行中的封裝。%n封裝執行個體識別碼: %1%n封裝識別碼: %2%n封裝名稱: %3%n封裝描述: %4%n封裝|服務正嘗試停止執行中的封裝。 您可以在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中監視並停止執行中的封裝。 如需如何在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中管理封裝的資訊，請參閱[封裝管理 &#40;SSIS 服務&#41;](../../integration-services/service/package-management-ssis-service.md)。|  

## <a name="view-events"></a>檢視事件
  目前有兩個工具可讓您用來檢視 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的事件：  
  
-   **中的** [記錄檔檢視器] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]對話方塊。 **[記錄檔檢視器]** 對話方塊包括匯出、篩選和搜尋記錄檔的選項。 如需 [記錄檔檢視器]**[ 中選項的詳細資訊，請參閱**記錄檔檢視器 F1 說明](../../relational-databases/logs/log-file-viewer-f1-help.md)。  
  
-   Windows 事件檢視器。  
  
 如需 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務所記錄之事件的描述，請參閱 [Integration Services 服務所記錄的事件](../../integration-services/service/events-logged-by-the-integration-services-service.md)。  
  
### <a name="to-view-service-events-for-integration-services-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中檢視 Integration Services 的服務事件  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
2.  在 **[檔案]** 功能表上，按一下 **[連接物件總管]**。  
  
3.  在 **[連接到伺服器]** 對話方塊中，選取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器類型，選取或尋找要連接的伺服器，然後按一下 **[連接]**。  
  
4.  在物件總管中，以滑鼠右鍵按一下 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，然後按一下 [檢視記錄]。  
  
5.  若要檢視 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 事件，請選取 **[SQL Server Integration Services]**。 **[NT 事件]** 選項會隨 **[SQL Server Integration Services]** 選項的選取和清除而自動選取和清除。  
  
### <a name="to-view-service-events-for-integration-services-in-windows-event-viewer"></a>在 Windows 事件檢視器中檢視 Integration Services 的服務事件  
  
1.  在 **[控制台]**中，如果您使用「一般檢視」，請按一下 **[系統管理工具]**，如果您使用「類別檢視」，請按一下 **[效能及維護]** ，然後按一下 **[系統管理工具]**。  
  
2.  按一下 **[事件檢視器]**。  
  
3.  在 **[事件檢視器]** 對話方塊中，按一下 **[應用程式]**。  
  
4.  在 [應用程式] 嵌入式管理單元中，尋找 [來源] 資料行中值為 **SQLISService** 的項目，以滑鼠右鍵按一下該項目，然後按一下 [屬性]。  
  
5.  選擇性地按一下向上箭頭或向下箭頭，以顯示上一個或下一個事件。  
  
6.  選擇性地按一下 [複製至剪貼簿] 圖示，以複製事件資訊。  
  
7.  選擇使用位元組或文字顯示事件資料。  
  
8.  按一下 **[確定]**。  
  
9. 在 **[檔案]** 功能表上，按一下 **[結束]** ，以關閉 **[事件檢視器]** 對話方塊。  
 
## <a name="related-tasks"></a>相關工作  
 如需如何檢視記錄項目的資訊，請參閱 [Integration Services 封裝所記錄的事件](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  

