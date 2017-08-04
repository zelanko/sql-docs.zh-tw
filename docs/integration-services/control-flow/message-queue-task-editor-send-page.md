---
title: "訊息佇列工作編輯器 （傳送頁面） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.msgqueuetask.send.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 565aa079-ac44-4407-8efc-cddab839de30
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d0914b6ab2222fa91d7db229970b081d4a43314d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="message-queue-task-editor-send-page"></a>訊息佇列工作編輯器 (傳送頁面)
  使用 **[訊息佇列工作編輯器]** 對話方塊的 **[傳送]** 頁面，即可設定從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝傳送訊息的訊息佇列工作。  
  
 若要了解這個工作，請參閱＜ [Message Queue Task](../../integration-services/control-flow/message-queue-task.md)＞。  
  
## <a name="options"></a>選項。  
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
  
|Value|說明|  
|-----------|-----------------|  
|**資料檔訊息**|訊息儲存在檔案中。 選取此值會顯示動態選項 **[DataFileMessage]**。|  
|**變數訊息**|訊息儲存在變數中。 選取此值會顯示動態選項 **[VariableMessage]**。|  
|**字串訊息**|訊息儲存在訊息佇列工作中。 選取此值會顯示動態選項 **[StringMessage]**。|  
  
## <a name="messagetype-dynamic-options"></a>MessageType 動態選項  
  
### <a name="messagetype--data-file-message"></a>MessageType = 資料檔訊息  
 **[DataFileMessage]**  
 輸入資料檔的路徑，或按一下省略符號 **(...)** ，然後再尋找檔案。  
  
### <a name="messagetype--variable-message"></a>MessageType = 變數訊息  
 **[VariableMessage]**  
 輸入變數名稱，或按一下省略符號 **(...)** ，然後再選取變數。 變數以逗號分隔。  
  
 **相關主題：** 選取變數  
  
### <a name="messagetype--string-message"></a>MessageType = 字串訊息  
 **[StringMessage]**  
 輸入字串訊息，或按一下省略符號 **(...)**，然後在 [輸入字串訊息] 對話方塊中輸入訊息。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [訊息佇列工作編輯器 &#40;一般頁面 &#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [訊息佇列工作編輯器 &#40;接收頁面 &#41;](../../integration-services/control-flow/message-queue-task-editor-receive-page.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
  
