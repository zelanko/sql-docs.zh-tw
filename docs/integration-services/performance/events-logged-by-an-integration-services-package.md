---
title: Integration Services 套件所記錄的事件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- package [Integration Services], events
- events [Integration Services], package
ms.assetid: 55a0951a-46f3-4f0f-9972-74cec9cc26b7
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dac55ba135fec92baeb845a2ee846f1840b0aa15
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="events-logged-by-an-integration-services-package"></a>Integration Services 封裝所記錄的事件
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝會將各種事件訊息記錄至 Windows 應用程式事件記錄檔。 當封裝啟動、停止以及發生特定問題時，此封裝就會記錄這些訊息。  
  
 本主題會提供封裝記錄至應用程式事件記錄檔之常見事件訊息的相關資訊。 根據預設，封裝會記錄其中某些訊息，即使您尚未針對此封裝啟用記錄也一樣。 不過，只有當您針對此封裝啟用記錄時，封裝才會記錄其他訊息。 不論此封裝預設記錄這些訊息或因為已經啟用記錄，訊息的事件來源都是 SQLISPackage。  
  
 如需如何執行 SSIS 套件的一般資訊，請參閱[執行專案和套件](../packages/run-integration-services-ssis-packages.md)。  
  
 如需如何針對執行中封裝進行疑難排解的詳細資訊，請參閱 [封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="messages-about-the-status-of-the-package"></a>封裝狀態的相關訊息  
 當您執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時，此封裝通常會記錄有關封裝進度和狀態的各種訊息。 下表將列出這些訊息。  
  
> [!NOTE]  
>  此封裝會記錄下表中的訊息，即使您尚未針對此封裝啟用記錄也一樣。  
  
|事件識別碼|符號名稱|文字|注意|  
|--------------|-------------------|----------|-----------|  
|12288|DTS_MSG_PACKAGESTART|封裝 "" 已啟動。|封裝已開始執行。|  
|12289|DTS_MSG_PACKAGESUCCESS|封裝 "" 已順利完成。|封裝執行成功，而且不再執行。|  
|12290|DTS_MSG_PACKAGECANCEL|封裝 "%1!s!" 已取消。|封裝不再執行，因為封裝已取消。|  
|12291|DTS_MSG_PACKAGEFAILURE|封裝 "" 失敗。|封裝無法執行成功，而且已停止執行。|  
  
 依預設，在新的安裝中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會設定為不要將與封裝執行相關的特定事件記錄至應用程式事件記錄檔。 當您使用最新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的資料收集器功能時，此設定可避免產生過多的事件記錄項目。 不會記錄的事件包括 EventID 12288「封裝已啟動」和 EventID 12289「封裝已成功完成」。 若要將這些事件記錄到應用程式事件記錄檔，請開啟登錄進行編輯。 在登錄中找出 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS 節點，然後將 LogPackageExecutionToEventLog 設定的 DWORD 值從 0 變更為 1。 不過， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在升級安裝中則是設為記錄這兩種事件。 若要停用記錄，請將 LogPackageExecutionToEventLog 設定的值從 1 設為 0。  
  
## <a name="messages-associated-with-package-logging"></a>與封裝記錄相關聯的訊息  
 如果您已經針對封裝啟用記錄，應用程式事件記錄檔就是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中選擇性記錄功能所支援的其中一個目的地。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
 當您已經針對封裝啟用記錄，而且記錄檔位置是應用程式事件記錄檔時，此封裝就會記錄有關下列資訊的項目：  
  
-   封裝執行時封裝所在階段的相關訊息。  
  
-   封裝執行時所發生之特定事件的相關訊息。  
  
### <a name="messages-about-the-stages-of-package-execution"></a>封裝執行階段的相關訊息  
  
|事件識別碼|符號名稱|文字|注意|  
|--------------|-------------------|----------|-----------|  
|12544|DTS_MSG_EVENTLOGENTRY|事件名稱: %1%r 訊息: %9%r 操作員: %2%r 來源名稱: %3%r 來源識別碼: %4%r 執行識別碼: %5%r 開始時間: %6%r 結束時間: %7%r 資料碼: %8|當您將封裝記錄設定為應用程式事件記錄檔時，各種訊息都會使用這個一般格式。|  
|12556|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|事件名稱: %1%r 訊息: %9%r 操作員: %2%r 來源名稱: %3%r 來源識別碼: %4%r 執行識別碼: %5%r 開始時間: %6%r 結束時間: %7%r 資料碼: %8|封裝已啟動。|  
|12547|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|事件名稱: %1%r 訊息: %9%r 操作員: %2%r 來源名稱: %3%r 來源識別碼: %4%r 執行識別碼: %5%r 開始時間: %6%r 結束時間: %7%r 資料碼: %8|物件的驗證即將開始。|  
|12548|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|事件名稱: %1%r 訊息: %9%r 操作員: %2%r 來源名稱: %3%r 來源識別碼: %4%r 執行識別碼: %5%r 開始時間: %6%r 結束時間: %7%r 資料碼: %8|物件的驗證已完成。|  
|12552|DTS_MSG_EVENTLOGENTRY_PROGRESS|事件名稱: %1%r 訊息: %9%r 操作員: %2%r 來源名稱: %3%r 來源識別碼: %4%r 執行識別碼: %5%r 開始時間: %6%r 結束時間: %7%r 資料碼: %8|這則一般訊息會報告封裝進度。|  
|12546|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|事件名稱: %1%r 訊息: %9%r 操作員: %2%r 來源名稱: %3%r 來源識別碼: %4%r 執行識別碼: %5%r 開始時間: %6%r 結束時間: %7%r 資料碼: %8|物件已經完成其工作。|  
|12557|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|事件名稱: %1%r 訊息: %9%r 操作員: %2%r 來源名稱: %3%r 來源識別碼: %4%r 執行識別碼: %5%r 開始時間: %6%r 結束時間: %7%r 資料碼: %8|封裝已經完成執行。|  
  
### <a name="messages-about-events-that-occur"></a>發生之事件的相關訊息  
 下表只會列出屬於事件結果的某些訊息。 如需 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所使用之錯誤、警告和參考用訊息的更完整清單，請參閱 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)。  
  
|事件識別碼|符號名稱|文字|注意|  
|--------------|-------------------|----------|-----------|  
|12251|DTS_MSG_EVENTLOGENTRY_TASKFAILED|事件名稱: %1%r 訊息: %9%r 操作員: %2%r 來源名稱: %3%r 來源識別碼: %4%r 執行識別碼: %5%r 開始時間: %6%r 結束時間: %7%r 資料碼: %8|工作失敗。|  
|12250|DTS_MSG_EVENTLOGENTRY_ERROR|事件名稱: %1%r 訊息: %9%r 操作員: %2%r 來源名稱: %3%r 來源識別碼: %4%r 執行識別碼: %5%r 開始時間: %6%r 結束時間: %7%r 資料碼: %8|這則訊息會報告已經發生的錯誤。|  
|12249|DTS_MSG_EVENTLOGENTRY_WARNING|事件名稱: %1%r 訊息: %9%r 操作員: %2%r 來源名稱: %3%r 來源識別碼: %4%r 執行識別碼: %5%r 開始時間: %6%r 結束時間: %7%r 資料碼: %8|這則訊息會報告已經發生的警告。|  
|12258|DTS_MSG_EVENTLOGENTRY_INFORMATION|事件名稱: %1%r 訊息: %9%r 操作員: %2%r 來源名稱: %3%r 來源識別碼: %4%r 執行識別碼: %5%r 開始時間: %6%r 結束時間: %7%r 資料碼: %8|這則訊息會報告與錯誤或警告沒有關聯的參考用訊息。|  

## <a name="view-log-entries-in-the-log-events-window"></a>檢視記錄事件視窗中的記錄項目
  此程序描述如何執行封裝並檢視封裝寫入的記錄項目。 您可以即時檢視記錄項目， 也可以複製及儲存寫入 [記錄事件] 視窗中的記錄項目，以執行進一步的分析。  
  
 您不需要將記錄項目寫入記錄檔，以便將項目寫入 [記錄事件] 視窗中。  
  
### <a name="to-view-log-entries"></a>檢視記錄項目  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [SSIS] 功能表上，按一下 [記錄事件]。 您可以將 View.LogEvents 命令對應到您在 [選項] 對話方塊的 [鍵盤] 頁面中所選擇的組合鍵，以選擇性地顯示 [記錄事件] 視窗。  
  
3.  在 **[偵錯]** 功能表上，按一下 **[開始偵錯]**。  
  
     當執行階段遇到為了記錄而啟用的事件與自訂訊息時，每個事件或訊息的記錄項目都會寫入 [記錄事件] 視窗。  
  
4.  在 **[偵錯]** 功能表上，按一下 **[停止偵錯]**。  
  
     記錄項目將繼續保留在 [記錄事件] 視窗中，直到您重新執行封裝、執行不同的封裝或關閉 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 為止。  
  
5.  檢視 [記錄事件] 視窗中的記錄項目。  
  
6.  (選擇性) 按一下要複製的記錄項目，按一下滑鼠右鍵，然後按一下 [複製]。  
  
7.  (選擇性) 按兩下記錄項目，然後在 [記錄項目] 對話方塊中檢視單一記錄項目的詳細資料。  
  
8.  在 [記錄項目] 對話方塊中，按一下上下箭頭以顯示上一個或下一個記錄項目，然後按一下複製圖示來複製記錄項目。  
  
9. 開啟文字編輯器、貼上，然後將記錄項目儲存為文字檔。
