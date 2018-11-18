---
title: 訊息佇列工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.messagequeuetask.f1
- sql13.dts.designer.msgqueuetask.general.f1
- sql13.dts.designer.msgqueuetask.send.f1
- sql13.dts.designer.msgqueuetask.receive.f1
- sql13.dts.designer.selectvariables.f1
helpviewer_keywords:
- Message Queue task [Integration Services]
- receiving messages
- messages [Integration Services]
- sending messages
ms.assetid: ae1d8fad-6649-4e93-b589-14a32d07da33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 61956bf22dc15c95d986317d3a3cf18e9ca4d58b
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51639885"
---
# <a name="message-queue-task"></a>Message Queue Task
  「訊息佇列」工作可讓您使用 Message Queuing (又稱為 MSMQ) 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝之間傳送和接收訊息，或將訊息傳送至由自訂應用程式處理的應用程式佇列。 這些訊息可採用簡單文字、檔案或變數及其值的形式。  
  
 透過使用「訊息佇列」工作，您可以協調整個企業內的作業。 如果目的地無法使用或者忙碌，可以將訊息排入佇列以稍後傳遞；例如，此工作可將屬於銷售代表離線之膝上型電腦的訊息排入佇列，等銷售代表們連接到網路後就可以接收到各自的訊息。 您可將「訊息佇列」工作用於下列用途：  
  
-   延遲工作執行，直到其他封裝簽入。 例如，在每個零售站台的夜間維護完成後，訊息佇列工作會傳送訊息給公司電腦。 執行於公司電腦的封裝將包含「訊息佇列」工作，每個工作都會等待來自特定零售站台的訊息。 來自站台的訊息抵達後，便會有一個工作自該站台上傳資料。 所有站台均簽入後，封裝會計算摘要總數。  
  
-   將資料檔傳送給處理它們的電腦。 例如，餐廳的收銀機輸出可以將資料檔訊息傳送至公司的薪資系統，以進行服務生的小費資料擷取。  
  
-   將檔案散發至整個企業。 例如，封裝可使用「訊息佇列」工作將封裝檔案傳送至另一台電腦。 接著，執行於目的電腦的封裝使用「訊息佇列」工作，以在本機擷取與儲存封裝。  
  
 傳送或接收訊息時，「訊息佇列」工作會使用下列四種訊息類型之一：資料檔、字串、字串訊息至變數或變數。 只有接收訊息時才能使用「字串訊息至變數」訊息類型。  
  
 工作使用 MSMQ 連接管理員以連接到訊息佇列。 如需詳細資訊，請參閱 [MSMQ 連線管理員](../../integration-services/connection-manager/msmq-connection-manager.md)。 如需有關 Message Queuing 的詳細資訊，請參閱 [MSDN Library](https://go.microsoft.com/fwlink/?LinkId=7022)。  
  
 「訊息佇列」工作要求安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。 您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈的 **[要安裝的元件]** 頁面或 **[特徵選取]** 頁面上選取要安裝的一些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件，會安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件的部分子集。 這些元件對特定的工作有用，但 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的功能會受到限制。 例如， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 選項會安裝設計某個封裝所需的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件，但不會安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務，因此「訊息佇列」工作將無法運作。 為了確保 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的完整安裝，您必須在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] [要安裝的元件] **頁面上選取** 。 如需安裝及執行「訊息佇列」工作的詳細資訊，請參閱 [安裝 Integration Services](../../integration-services/install-windows/install-integration-services.md)。  
  
> [!NOTE]  
>  當電腦的作業系統是以 FIPS 模式設定並且工作使用加密時，「訊息佇列」工作無法符合美國聯邦資訊處理標準 (FIPS) 140-2 的規定。 如果「訊息佇列」工作沒有使用加密，工作會順利執行。  
  
## <a name="message-types"></a>訊息類型  
 您可利用下列方式設定「訊息佇列」工作提供的訊息類型：  
  
-   **Data file** 訊息指定某個檔案包含訊息。 接收訊息時，您可以設定工作以儲存檔案，覆寫現有的檔案，並指定工作可以從中接收訊息的封裝。  
  
-   **String** 訊息指定訊息為字串。 接收訊息時，您可以設定工作，以比較接收到的字串與使用者自訂字串，並根據比較結果採取行動。 字串比較可以為完全相符、區分大小寫或不區分大小寫，或者使用子字串。  
  
-   **String message to variable** 將來源訊息指定為傳送到目的變數的字串。 您可以設定工作使用完全相符、不區分大小寫或子字串比較，來比較接收到的字串與使用者自訂的字串。 只有當工作接收訊息時此訊息類型才可用。  
  
-   **Variable** 指定訊息將包含一或多個變數。 您可以設定工作，以指定訊息中包含的變數名稱。 接收訊息時您可以設定工作，以指定可從中接收訊息的封裝，以及做為訊息目的地的變數。  
  
## <a name="sending-messages"></a>傳送訊息  
 設定「訊息佇列」工作以傳送訊息時，您可以使用 Message Queuing 技術目前支援的加密演算碼 RC2 及 RC4 其中一個，以加密訊息。 這兩種加密演算法目前被認為在密碼編譯技術上不如較新的演算法，不過 Message Queuing 技術目前還不支援較新的演算法。 因此，在使用「訊息佇列」工作傳送訊息時，應仔細考慮您的加密需求。  
  
## <a name="receiving-messages"></a>接收訊息  
 接收訊息時，可以利用下列方式設定「訊息佇列」工作。  
  
-   略過訊息，或者從佇列中移除訊息。  
  
-   指定逾時。  
  
-   若逾時發生則失敗。  
  
-   如果訊息儲存在 **Data file**中則覆寫現有的檔案。  
  
-   如果訊息使用 **Data file message** 類型，則以不同的檔案名稱儲存訊息檔案。  
  
## <a name="custom-logging-messages-available-on-the-message-queue-task"></a>訊息佇列工作上可用的自訂記錄訊息  
 下表列出「訊息佇列」工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|Description|  
|---------------|-----------------|  
|**MSMQAfterOpen**|指出工作已經完成開啟訊息佇列。|  
|**MSMQBeforeOpen**|指出工作已經開始開啟訊息佇列。|  
|**MSMQBeginReceive**|指出工作已經開始接收訊息。|  
|**MSMQBeginSend**|指出工作已經開始傳送訊息。|  
|**MSMQEndReceive**|指出工作已經完成接收訊息。|  
|**MSMQEndSend**|指出工作已經完成傳送訊息。|  
|**MSMQTaskInfo**|提供有關工作的描述性資訊。|  
|**MSMQTaskTimeOut**|指出工作已經逾時。|  
  
## <a name="configuration-of-the-message-queue-task"></a>訊息佇列工作的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。 如需有關可在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列主題：  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關以程式設計方式來設定這些屬性的詳細資訊，請參閱《開發人員指南》中 **Microsoft.SqlServer.Dts.Tasks.MessageQueueTask.MessageQueueTask** 類別的文件。  
  
## <a name="related-tasks"></a>相關工作  
 如需如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定這些屬性的詳細資訊，請參閱 [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)。  
  
## <a name="message-queue-task-editor-general-page"></a>訊息佇列工作編輯器 (一般頁面)
  使用 **[訊息佇列工作編輯器]** 對話方塊的 **[一般頁面]** ，即可命名和描述訊息佇列工作、指定訊息格式以及指出工作是否傳送或接收訊息。  
  
### <a name="options"></a>選項。  
 **名稱**  
 為訊息佇列工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入訊息佇列工作的描述。  
  
 **Use2000Format**  
 指示是否使用 Message Queuing (又稱為 MSMQ) 的 2000 格式。 預設值為 **False**。  
  
 **MSMQConnection**  
 選取現有的 MSMQ 連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題**： [MSMQ 連線管理員](../../integration-services/connection-manager/msmq-connection-manager.md)、 [MSMQ 連線管理員編輯器](../../integration-services/connection-manager/msmq-connection-manager-editor.md)  
  
 **訊息**  
 指定訊息佇列工作是否傳送或接收訊息。 如果選取 **[傳送訊息]**，對話方塊的左窗格會列出 [傳送] 頁面，如果選取 **[接收訊息]**，則會列出 [接收] 頁面。 依預設，此值設定為 **[傳送訊息]**。  
  
## <a name="message-queue-task-editor-send-page"></a>訊息佇列工作編輯器 (傳送頁面)
  使用 **[訊息佇列工作編輯器]** 對話方塊的 **[傳送]** 頁面，即可設定從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝傳送訊息的訊息佇列工作。  
  
### <a name="options"></a>選項。  
 **UseEncryption**  
 指出是否要加密訊息。 預設值為 **False**。  
  
 **EncryptionAlgorithm**  
 如果您選擇使用加密，請指定要使用之加密演算法的名稱。 「訊息佇列」工作可以使用 RC2 和 RC4 演算法。 預設值是 **[RC2]**。  
  
> [!NOTE]  
>  只有 RC4 演算法支援回溯相容性。 只有在資料庫相容性層級為 90 或 100 時，才能使用 RC4 或 RC4_128 加密新資料  (不建議使用)。請改用較新的演算法，例如其中一個 AES 演算法。 在最新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，使用 RC4 或 RC4_128 加密的資料，可以在任何相容性層級進行解密。  
  
> [!IMPORTANT]  
>  這些是 Message Queuing (又稱為 MSMQ) 技術支援的加密演算法。 這兩種加密演算法目前被認為在密碼編譯技術上不如較新的演算法，不過 Message Queuing 目前還不支援較新的演算法。 因此，在使用「訊息佇列」工作傳送訊息時，應仔細考慮您的加密需求。  
  
 **MessageType**  
 選取訊息類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**資料檔訊息**|訊息儲存在檔案中。 選取此值會顯示動態選項 **[DataFileMessage]**。|  
|**變數訊息**|訊息儲存在變數中。 選取此值會顯示動態選項 **[VariableMessage]**。|  
|**字串訊息**|訊息儲存在訊息佇列工作中。 選取此值會顯示動態選項 **[StringMessage]**。|  
  
### <a name="messagetype-dynamic-options"></a>MessageType 動態選項  
  
#### <a name="messagetype--data-file-message"></a>MessageType = 資料檔訊息  
 **[DataFileMessage]**  
 輸入資料檔的路徑，或按一下省略符號 **(...)** ，然後再尋找檔案。  
  
#### <a name="messagetype--variable-message"></a>MessageType = 變數訊息  
 **[VariableMessage]**  
 輸入變數名稱，或按一下省略符號 **(...)** ，然後再選取變數。 變數以逗號分隔。  
  
 **相關主題：** 選取變數  
  
#### <a name="messagetype--string-message"></a>MessageType = 字串訊息  
 **[StringMessage]**  
 輸入字串訊息，或按一下省略符號 **(...)**，然後在 [輸入字串訊息] 對話方塊中輸入訊息。  
  
## <a name="message-queue-task-editor-receive-page"></a>訊息佇列工作編輯器 (接收頁面)
  使用 [訊息佇列工作編輯器] 對話方塊的 [接收] 頁面，即可設定訊息佇列工作，以接收 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ) 訊息。  
  
### <a name="options"></a>選項。  
 **RemoveFromMessageQueue**  
 指出接收訊息之後，是否從佇列中移除該訊息。 此值預設為 **False**。  
  
 **ErrorIfMessageTimeOut**  
 指出當訊息逾時的時侯工作是否失敗，並顯示錯誤訊息。 預設值為 **False**。  
  
 **TimeoutAfter**  
 如果您選擇在工作失敗時要顯示錯誤訊息，請指定顯示逾時訊息之前要等候的秒數。  
  
 **MessageType**  
 選取訊息類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**資料檔訊息**|訊息儲存在檔案中。 選取此值會顯示動態選項 **[DataFileMessage]**。|  
|**變數訊息**|訊息儲存在變數中。 選取此值會顯示動態選項 **[VariableMessage]**。|  
|**字串訊息**|訊息儲存在訊息佇列工作中。 選取此值會顯示動態選項 **[StringMessage]**。|  
|**字串訊息至變數**|訊息<br /><br /> 選取此值會顯示動態選項 **[StringMessage]**。|  
  
### <a name="messagetype-dynamic-options"></a>MessageType 動態選項  
  
#### <a name="messagetype--data-file-message"></a>MessageType = 資料檔訊息  
 **SaveFileAs**  
 輸入要使用的檔案路徑，或按一下省略符號按鈕 **(…)** ，然後尋找檔案。  
  
 **Overwrite**  
 指出儲存資料檔訊息的內容時，是否要覆寫現有檔案中的資料。 預設值為 **False**。  
  
 **篩選**  
 指定是否要將篩選套用至訊息。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**沒有篩選**|工作不會篩選訊息。 選取此值會顯示動態選項 **IdentifierReadOnly**。|  
|**來自封裝**|訊息只接收來自指定之封裝的訊息。 選取此值會顯示動態選項 **識別碼**＞。|  
  
#### <a name="filter-dynamic-options"></a>篩選動態選項  
  
##### <a name="filter--no-filter"></a>篩選 = 沒有篩選  
 **IdentifierReadOnly**  
 此選項是唯讀的。 當先前有設定篩選屬性時，此選項可能是空白或包含封裝的 GUID。  
  
##### <a name="filter--from-package"></a>篩選 = 來自封裝  
 **識別碼**  
 如果您選擇套用篩選，請輸入可以接收訊息之來源封裝的唯一識別碼，或者按一下省略符號按鈕 **(…)** ，然後指定封裝。  
  
 **相關主題：**[選取封裝](../../integration-services/control-flow/select-a-package.md)  
  
#### <a name="messagetype--variable-message"></a>MessageType = 變數訊息  
 **篩選**  
 指定是否要將篩選套用至訊息。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**沒有篩選**|工作不會篩選訊息。 選取此值會顯示動態選項 **IdentifierReadOnly**。|  
|**來自封裝**|訊息只接收來自指定之封裝的訊息。 選取此值會顯示動態選項 **識別碼**＞。|  
  
 **變數**  
 鍵入變數名稱，或按一下 [\<新增變數…>]，然後設定新的變數。  
  
 **相關主題：**[加入變數](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="filter-dynamic-options"></a>篩選動態選項  
  
##### <a name="filter--no-filter"></a>篩選 = 沒有篩選  
 **IdentifierReadOnly**  
 此選項是空白。  
  
##### <a name="filter--from-package"></a>篩選 = 來自封裝  
 **識別碼**  
 如果您選擇套用篩選，請輸入可以接收訊息之來源封裝的唯一識別碼，或者按一下省略符號按鈕 **(…)** ，然後指定封裝。  
  
 **相關主題：**[選取封裝](../../integration-services/control-flow/select-a-package.md)  
  
#### <a name="messagetype--string-message"></a>MessageType = 字串訊息  
 **比較**  
 指定是否要將篩選套用至訊息。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**無**|不會比較訊息。|  
|**完全相符**|訊息必須與 **CompareString** 選項中的字串完全相符。|  
|**忽略大小寫**|訊息必須與 **CompareString** 選項中的字串相符，但是比較時不會區分大小寫。|  
|**包含**|訊息必須包含 **CompareString** 選項中的字串。|  
  
 **CompareString**  
 除非 [比較] 選項設定為 [無]，否則請提供訊息要比較的字串。  
  
#### <a name="messagetype--string-message-to-variable"></a>MessageType = 字串訊息至變數  
 **比較**  
 指定是否要將篩選套用至訊息。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**無**|不會比較訊息。|  
|**完全相符**|訊息必須與 **CompareString** 選項中的字串完全相符。|  
|**忽略大小寫**|訊息必須與 **CompareString** 選項中的字串相符，但是比較時不會區分大小寫。|  
|**包含**|訊息必須包含 **CompareString** 選項中的字串。|  
  
 **CompareString**  
 除非 [比較] 選項設定為 [無]，否則請提供訊息要比較的字串。  
  
 **變數**  
 鍵入要保存已接收之訊息的變數名稱，或按一下 [\<新增變數…>]，然後設定新的變數。  
  
 **相關主題：**[加入變數](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="select-variables"></a>選取變數
  使用 [選取變數] 對話方塊，即可指定在訊息佇列工作中用於傳送訊息作業的變數。 [可用的變數] 清單包含在訊息佇列工作或其父容器之範圍中的系統和使用者自訂變數。 此工作使用 [選取的變數] 清單中的變數。  
  
### <a name="options"></a>選項。  
 **可用的變數**  
 選取一個或多個變數。  
  
 **選取的變數**  
 選取一個或多個變數。  
  
 **向右鍵**  
 將選取的變數移至 [選取的變數] 清單。  
  
 **向左鍵**  
 將選取的變數移回到 [可用的變數] 清單。  
  
 **新增變數**  
 建立新變數。  
  
 **相關主題：**[加入變數](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
