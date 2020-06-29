---
title: 傳送錯誤訊息工作編輯器（訊息頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfererrormessagestask.errormessages.F1
helpviewer_keywords:
- Transfer Error Messages Task Editor
ms.assetid: cb2226a0-3037-4fdf-966f-81eabc0da9cf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7b551d60d36948cb4c950dfcd9a17e2c16229420
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85420695"
---
# <a name="transfer-error-messages-task-editor-messages-page"></a>傳送錯誤訊息工作編輯器 (訊息頁面)
  使用 [傳送錯誤訊息工作編輯器]**** 對話方塊的 [訊息]**** 頁面，即可指定屬性用來將一或多個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用者自訂錯誤訊息，從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的一個執行個體複製到另一個。 如需這項工作的詳細資訊，請參閱 [傳送錯誤訊息工作](control-flow/transfer-error-messages-task.md)。  
  
## <a name="options"></a>選項  
 **SourceConnection**  
 在清單中選取 SMO 連線管理員，或按一下 **\<New connection...>** 以建立與來源伺服器的新連接。  
  
 **[Destinationconnection**  
 在清單中選取 SMO 連線管理員，或按一下 **\<New connection...>** 以建立目的地伺服器的新連接。  
  
 **IfObjectExists**  
 如果有相同名稱的錯誤訊息已存在於目的地伺服器上，選取工作應覆寫現有使用者自訂錯誤訊息、略過現有訊息，或是失敗。  
  
 **TransferAllErrorMessages**  
 選取工作應將所有的訊息或只有指定的使用者自訂訊息，從來源伺服器複製到目的地伺服器。  
  
 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**True**|複製所有的使用者自訂訊息。|  
|**False**|只複製指定的使用者自訂訊息。|  
  
 **ErrorMessagesList**  
 按一下瀏覽按鈕 **（[...]）** 以選取要複製的錯誤訊息。  
  
> [!NOTE]  
>  您必須先指定 [SourceConnection]****，才能選取要複製的錯誤訊息。  
  
 **ErrorMessageLanguagesList**  
 按一下瀏覽按鈕 **（[...]）** ，以選取要將使用者定義的錯誤訊息複製到目的地伺服器的語言。 在您可以傳送其他語言版本的訊息至目的地伺服器之前，us_english (字碼頁 1033) 版的訊息必須存在於該伺服器上。  
  
> [!NOTE]  
>  您必須先指定 [SourceConnection]****，才能選取要複製的錯誤訊息。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 工作](control-flow/integration-services-tasks.md)   
 [傳送錯誤訊息工作編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [SMO 連線管理員](connection-manager/smo-connection-manager.md)   
 [傳送錯誤訊息工作編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [SMO 連線管理員](connection-manager/smo-connection-manager.md)  
  
  
