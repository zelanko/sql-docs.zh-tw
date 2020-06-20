---
title: 訊息佇列工作編輯器（傳送頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.send.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 565aa079-ac44-4407-8efc-cddab839de30
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2ed0d210668b64ff6f6fcc8c94a713743e2f9bfa
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84951048"
---
# <a name="message-queue-task-editor-send-page"></a>訊息佇列工作編輯器 (傳送頁面)
  使用 [訊息佇列工作編輯器]**** 對話方塊的 [傳送]**** 頁面，即可設定從 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 套件傳送訊息的「訊息佇列」工作。  
  
 若要了解這個工作，請參閱＜ [Message Queue Task](control-flow/message-queue-task.md)＞。  
  
## <a name="options"></a>選項。  
 **UseEncryption**  
 指出是否要加密訊息。 預設值為 `False`。  
  
 **EncryptionAlgorithm**  
 如果您選擇使用加密，請指定要使用之加密演算法的名稱。 「訊息佇列」工作可以使用 RC2 和 RC4 演算法。 預設值是 **[RC2]**。  
  
> [!NOTE]  
>  只有 RC4 演算法支援回溯相容性。 只有在資料庫相容性層級為 90 或 100 時，才能使用 RC4 或 RC4_128 加密新資料  (不建議使用)。請改用較新的演算法，例如其中一個 AES 演算法。 在最新版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中，使用 RC4 或 RC4_128 加密的資料，可以在任何相容性層級進行解密。  
  
> [!IMPORTANT]  
>  這些是 Message Queuing (又稱為 MSMQ) 技術支援的加密演算法。 這兩種加密演算法目前被認為在密碼編譯技術上不如較新的演算法，不過 Message Queuing 目前還不支援較新的演算法。 因此，在使用「訊息佇列」工作傳送訊息時，應仔細考慮您的加密需求。  
  
 **MessageType**  
 選取訊息類型。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**資料檔訊息**|訊息儲存在檔案中。 選取此值會顯示動態選項 **[DataFileMessage]**。|  
|**變數訊息**|訊息儲存在變數中。 選取此值會顯示動態選項 **[VariableMessage]**。|  
|**字串訊息**|訊息儲存在訊息佇列工作中。 選取此值會顯示動態選項 **[StringMessage]**。|  
  
## <a name="messagetype-dynamic-options"></a>MessageType 動態選項  
  
### <a name="messagetype--data-file-message"></a>MessageType = 資料檔訊息  
 **[DataFileMessage]**  
 輸入資料檔案的路徑，或按一下省略號 **（...）** ，然後找出檔案。  
  
### <a name="messagetype--variable-message"></a>MessageType = 變數訊息  
 **[VariableMessage]**  
 輸入變數名稱，或按一下省略號 **（...）** ，然後選取變數。 變數以逗號分隔。  
  
 **相關主題：** 選取變數  
  
### <a name="messagetype--string-message"></a>MessageType = 字串訊息  
 **[StringMessage]**  
 輸入字串訊息，或按一下省略號 **（...）** ，然後在 [**輸入字串訊息**] 對話方塊中輸入訊息。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[訊息佇列工作編輯器] &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [[訊息佇列工作編輯器] &#40;接收頁面&#41;](../../2014/integration-services/message-queue-task-editor-receive-page.md)   
 [運算式頁面](expressions/expressions-page.md)  
  
  
