---
title: 傳送郵件工作編輯器 （郵件頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sendmailtask.mail.f1
helpviewer_keywords:
- Send Mail Task Editor
ms.assetid: adb385d5-ef24-4d18-b9ea-b39e00a7075e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d80ca8e475bf9c2b56c11118a44e5282573f280d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66055824"
---
# <a name="send-mail-task-editor-mail-page"></a>傳送郵件工作編輯器 (郵件頁面)
  使用 [傳送郵件工作編輯器] 對話方塊的 [郵件] 頁面，即可指定收件者、訊息類型以及訊息的優先權。 您也可以附加檔案至訊息。 訊息文字可以是您提供的字串、包含文字之檔案的檔案連接，或包含文字之變數的名稱。  
  
 若要了解這項工作，請參閱 [傳送郵件工作](control-flow/send-mail-task.md)。  
  
## <a name="options"></a>選項。  
 **SMTPConnection**  
 在清單中選取 SMTP 連線管理員，或按一下 [\<新增連線...>]，即可建立新的連線管理員。  
  
> [!IMPORTANT]  
>  SMTP 連接管理員僅支援匿名驗證和 Windows 驗證， 而不支援基本驗證。  
  
 **相關主題：**[SMTP 連線管理員](connection-manager/smtp-connection-manager.md)  
  
 **來源**  
 指定寄件者的電子郵件地址。  
  
 **若要**  
 提供收件者的電子郵件地址，以分號分隔。  
  
 **副本**  
 指定也會收到訊息副本之個人的電子郵件地址，以分號分隔。  
  
 **密件副本**  
 指定也會收到訊息密件副本 (Bcc) 之個人的電子郵件地址，以分號分隔。  
  
 **主旨**  
 提供電子郵件訊息的主旨。  
  
 **MessageSourceType**  
 選取訊息的來源類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|將來源設定為訊息文字。 選取此值會顯示動態選項 [MessageSource]。|  
|**檔案連接**|將來源設定為包含訊息文字的檔案。 選取此值會顯示動態選項 [MessageSource]。|  
|**變數**|將來源設定為包含訊息文字的變數。 選取此值會顯示動態選項 [MessageSource]。|  
  
 **優先權**  
 設定訊息的優先權。  
  
 **附加檔案**  
 提供電子郵件訊息之附加檔案的檔案名稱，以垂直線 (|) 字元分隔。  
  
> [!NOTE]  
>  根據網際網路標準，[收件者]、[副本] 和 [密件副本] 欄位限制為 256 個字元。  
  
## <a name="messagesourcetype-dynamic-options"></a>MessageSourceType 動態選項  
  
### <a name="messagesourcetype--direct-input"></a>MessageSourceType = 直接輸入  
 **MessageSource**  
 輸入訊息文字或按一下瀏覽按鈕 ([...])，然後在 [訊息來源] 對話方塊中輸入訊息。  
  
### <a name="messagesourcetype--file-connection"></a>MessageSourceType = 檔案連接  
 **MessageSource**  
 在清單中選取檔案連線管理員，或按一下 [\<新增連線...>]，即可建立新的連線管理員。  
  
 **相關主題：**[檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="messagesourcetype--variable"></a>MessageSourceType = 變數  
 **MessageSource**  
 在清單中選取變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題：**[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [傳送郵件工作編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [運算式頁面](expressions/expressions-page.md)  
  
  
