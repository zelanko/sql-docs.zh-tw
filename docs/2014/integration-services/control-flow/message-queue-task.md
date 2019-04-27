---
title: 訊息佇列工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.messagequeuetask.f1
helpviewer_keywords:
- Message Queue task [Integration Services]
- receiving messages
- messages [Integration Services]
- sending messages
ms.assetid: ae1d8fad-6649-4e93-b589-14a32d07da33
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e7857294534f1c3c434f43c302cee8864925d953
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62831475"
---
# <a name="message-queue-task"></a>Message Queue Task
  「訊息佇列」工作可讓您使用 Message Queuing (又稱為 MSMQ) 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝之間傳送和接收訊息，或將訊息傳送至由自訂應用程式處理的應用程式佇列。 這些訊息可採用簡單文字、檔案或變數及其值的形式。  
  
 透過使用「訊息佇列」工作，您可以協調整個企業內的作業。 如果目的地無法使用或者忙碌，可以將訊息排入佇列以稍後傳遞；例如，此工作可將屬於銷售代表離線之膝上型電腦的訊息排入佇列，等銷售代表們連接到網路後就可以接收到各自的訊息。 您可將「訊息佇列」工作用於下列用途：  
  
-   延遲工作執行，直到其他封裝簽入。 例如，在每個零售站台的夜間維護完成後，訊息佇列工作會傳送訊息給公司電腦。 執行於公司電腦的封裝將包含「訊息佇列」工作，每個工作都會等待來自特定零售站台的訊息。 來自站台的訊息抵達後，便會有一個工作自該站台上傳資料。 所有站台均簽入後，封裝會計算摘要總數。  
  
-   將資料檔傳送給處理它們的電腦。 例如，餐廳的收銀機輸出可以將資料檔訊息傳送至公司的薪資系統，以進行服務生的小費資料擷取。  
  
-   將檔案散發至整個企業。 例如，封裝可使用「訊息佇列」工作將封裝檔案傳送至另一台電腦。 接著，執行於目的電腦的封裝使用「訊息佇列」工作，以在本機擷取與儲存封裝。  
  
 傳送或接收訊息時，「訊息佇列」工作會使用下列四種訊息類型之一：資料檔、字串、字串訊息至變數或變數。 只有接收訊息時才能使用「字串訊息至變數」訊息類型。  
  
 工作使用 MSMQ 連接管理員以連接到訊息佇列。 如需詳細資訊，請參閱 [MSMQ 連線管理員](../connection-manager/msmq-connection-manager.md)。 如需有關 Message Queuing 的詳細資訊，請參閱 [MSDN Library](https://go.microsoft.com/fwlink/?LinkId=7022)。  
  
 「訊息佇列」工作要求安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。 您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈的 **[要安裝的元件]** 頁面或 **[特徵選取]** 頁面上選取要安裝的一些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件，會安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件的部分子集。 這些元件對特定的工作有用，但 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的功能會受到限制。 例如， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 選項會安裝設計某個封裝所需的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件，但不會安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務，因此「訊息佇列」工作將無法運作。 為了確保 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的完整安裝，您必須在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] [要安裝的元件] **頁面上選取** 。 如需安裝及執行「訊息佇列」工作的詳細資訊，請參閱 [安裝 Integration Services](../install-windows/install-integration-services.md)。  
  
> [!NOTE]  
>  當電腦的作業系統是以 FIPS 模式設定並且工作使用加密時，「訊息佇列」工作無法符合美國聯邦資訊處理標準 (FIPS) 140-2 的規定。 如果「訊息佇列」工作沒有使用加密，工作會順利執行。  
  
## <a name="message-types"></a>訊息類型  
 您可利用下列方式設定「訊息佇列」工作提供的訊息類型：  
  
-   `Data file` 訊息指定某個檔案包含訊息。 接收訊息時，您可以設定工作以儲存檔案，覆寫現有的檔案，並指定工作可以從中接收訊息的封裝。  
  
-   `String` 訊息指定訊息為字串。 接收訊息時，您可以設定工作，以比較接收到的字串與使用者自訂字串，並根據比較結果採取行動。 字串比較可以為完全相符、區分大小寫或不區分大小寫，或者使用子字串。  
  
-   `String message to variable` 將來源訊息指定為傳送到目的變數的字串。 您可以設定工作使用完全相符、不區分大小寫或子字串比較，來比較接收到的字串與使用者自訂的字串。 只有當工作接收訊息時此訊息類型才可用。  
  
-   `Variable` 指定訊息將包含一或多個變數。 您可以設定工作，以指定訊息中包含的變數名稱。 接收訊息時您可以設定工作，以指定可從中接收訊息的封裝，以及做為訊息目的地的變數。  
  
## <a name="sending-messages"></a>傳送訊息  
 設定「訊息佇列」工作以傳送訊息時，您可以使用 Message Queuing 技術目前支援的加密演算碼 RC2 及 RC4 其中一個，以加密訊息。 這兩種加密演算法目前被認為在密碼編譯技術上不如較新的演算法，不過 Message Queuing 技術目前還不支援較新的演算法。 因此，在使用「訊息佇列」工作傳送訊息時，應仔細考慮您的加密需求。  
  
## <a name="receiving-messages"></a>接收訊息  
 接收訊息時，可以利用下列方式設定「訊息佇列」工作。  
  
-   略過訊息，或者從佇列中移除訊息。  
  
-   指定逾時。  
  
-   若逾時發生則失敗。  
  
-   如果訊息儲存在 `Data file` 中則覆寫現有的檔案。  
  
-   如果訊息使用 `Data file message` 類型，則以不同的檔案名稱儲存訊息檔案。  
  
## <a name="custom-logging-messages-available-on-the-message-queue-task"></a>訊息佇列工作上可用的自訂記錄訊息  
 下表列出「訊息佇列」工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)和[自訂訊息以進行記錄](../custom-messages-for-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`MSMQAfterOpen`|指出工作已經完成開啟訊息佇列。|  
|`MSMQBeforeOpen`|指出工作已經開始開啟訊息佇列。|  
|`MSMQBeginReceive`|指出工作已經開始接收訊息。|  
|`MSMQBeginSend`|指出工作已經開始傳送訊息。|  
|`MSMQEndReceive`|指出工作已經完成接收訊息。|  
|`MSMQEndSend`|指出工作已經完成傳送訊息。|  
|`MSMQTaskInfo`|提供有關工作的描述性資訊。|  
|`MSMQTaskTimeOut`|指出工作已經逾時。|  
  
## <a name="configuration-of-the-message-queue-task"></a>訊息佇列工作的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [訊息佇列工作編輯器 &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [訊息佇列工作編輯器 &#40;接收頁面&#41;](../message-queue-task-editor-receive-page.md)  
  
-   [訊息佇列工作編輯器 &#40;傳送頁面&#41;](../message-queue-task-editor-send-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關以程式設計方式來設定這些屬性的詳細資訊，請參閱《開發人員指南》中 **Microsoft.SqlServer.Dts.Tasks.MessageQueueTask.MessageQueueTask** 類別的文件。  
  
## <a name="related-tasks"></a>相關工作  
 如需如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定這些屬性的詳細資訊，請參閱 [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](integration-services-tasks.md)   
 [控制流程](control-flow.md)  
  
  
