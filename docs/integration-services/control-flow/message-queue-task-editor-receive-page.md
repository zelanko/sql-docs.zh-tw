---
title: "訊息佇列工作編輯器 (接收頁面) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.msgqueuetask.receive.f1"
helpviewer_keywords: 
  - "訊息佇列工作編輯器"
ms.assetid: 7028756d-1dcc-480c-bbcd-e9654f0772a0
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# 訊息佇列工作編輯器 (接收頁面)
  使用 [訊息佇列工作編輯器] 對話方塊的 [接收] 頁面，即可設定訊息佇列工作，以接收 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ) 訊息。  
  
 若要了解這個工作，請參閱＜ [Message Queue Task](../../integration-services/control-flow/message-queue-task.md)＞。  
  
## 選項。  
 **RemoveFromMessageQueue**  
 指出接收訊息之後，是否從佇列中移除該訊息。 此值預設為 **False**。  
  
 **ErrorIfMessageTimeOut**  
 指出當訊息逾時的時侯工作是否失敗，並顯示錯誤訊息。 預設值為 **False**。  
  
 **TimeoutAfter**  
 如果您選擇在工作失敗時要顯示錯誤訊息，請指定顯示逾時訊息之前要等候的秒數。  
  
 **MessageType**  
 選取訊息類型。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**資料檔訊息**|訊息儲存在檔案中。 選取此值會顯示動態選項 **[DataFileMessage]**。|  
|**變數訊息**|訊息儲存在變數中。 選取此值會顯示動態選項 **[VariableMessage]**。|  
|**字串訊息**|訊息儲存在訊息佇列工作中。 選取此值會顯示動態選項 **[StringMessage]**。|  
|**字串訊息至變數**|訊息<br /><br /> 選取此值會顯示動態選項 **[StringMessage]**。|  
  
## MessageType 動態選項  
  
### MessageType = 資料檔訊息  
 **SaveFileAs**  
 輸入要使用的檔案路徑，或按一下省略符號按鈕 **(…)**，然後尋找檔案。  
  
 **Overwrite**  
 指出儲存資料檔訊息的內容時，是否要覆寫現有檔案中的資料。 預設值為 **False**。  
  
 **篩選**  
 指定是否要將篩選套用至訊息。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**沒有篩選**|工作不會篩選訊息。 選取此值會顯示動態選項 [IdentifierReadOnly]。|  
|**來自封裝**|訊息只接收來自指定之封裝的訊息。 選取此值會顯示動態選項 [識別碼]。|  
  
### 篩選動態選項  
  
#### 篩選 = 沒有篩選  
 **IdentifierReadOnly**  
 此選項是唯讀的。 當先前有設定篩選屬性時，此選項可能是空白或包含封裝的 GUID。  
  
#### 篩選 = 來自封裝  
 **識別碼**  
 如果您選擇套用篩選，請輸入可以接收訊息之來源封裝的唯一識別碼，或者按一下省略符號按鈕 **(…)**，然後指定封裝。  
  
 **相關主題：**[選取封裝](../../integration-services/control-flow/select-a-package.md)  
  
### MessageType = 變數訊息  
 **篩選**  
 指定是否要將篩選套用至訊息。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**沒有篩選**|工作不會篩選訊息。 選取此值會顯示動態選項 **IdentifierReadOnly**。|  
|**來自封裝**|訊息只接收來自指定之封裝的訊息。 選取此值會顯示動態選項 [識別碼]。|  
  
 **變數**  
 輸入變數名稱，或按一下 [\<新增變數…>]，然後設定新的變數。  
  
 **相關主題：**[加入變數](../Topic/Add%20Variable.md)  
  
### 篩選動態選項  
  
#### 篩選 = 沒有篩選  
 **IdentifierReadOnly**  
 此選項是空白。  
  
#### 篩選 = 來自封裝  
 **識別碼**  
 如果您選擇套用篩選，請輸入可以接收訊息之來源封裝的唯一識別碼，或者按一下省略符號按鈕 **(…)**，然後指定封裝。  
  
 **相關主題：**[選取封裝](../../integration-services/control-flow/select-a-package.md)  
  
### MessageType = 字串訊息  
 **比較**  
 指定是否要將篩選套用至訊息。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**無**|不會比較訊息。|  
|**完全相符**|訊息必須與 **CompareString** 選項中的字串完全相符。|  
|**忽略大小寫**|訊息必須與 **CompareString** 選項中的字串相符，但是比較時不會區分大小寫。|  
|**包含**|訊息必須包含 **CompareString** 選項中的字串。|  
  
 **CompareString**  
 除非 [比較] 選項設定為 [無]，否則請提供訊息要比較的字串。  
  
### MessageType = 字串訊息至變數  
 **比較**  
 指定是否要將篩選套用至訊息。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**無**|不會比較訊息。|  
|**完全相符**|訊息必須與 **CompareString** 選項中的字串完全相符。|  
|**忽略大小寫**|訊息必須與 **CompareString** 選項中的字串相符，但是比較時不會區分大小寫。|  
|**包含**|訊息必須包含 **CompareString** 選項中的字串。|  
  
 **CompareString**  
 除非 [比較] 選項設定為 [無]，否則請提供訊息要比較的字串。  
  
 **變數**  
 輸入要保存已接收之訊息的變數名稱，或按一下 [\<新增變數…>]，然後設定新的變數。  
  
 **相關主題：**[加入變數](../Topic/Add%20Variable.md)  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [訊息佇列工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [訊息佇列工作編輯器 &#40;傳送頁面&#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)   
 [訊息佇列工作](../../integration-services/control-flow/message-queue-task.md)  
  
  