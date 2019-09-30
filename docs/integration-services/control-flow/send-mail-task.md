---
title: 傳送電子郵件工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sendmailtask.f1
- sql13.dts.designer.sendmailtask.general.f1
- sql13.dts.designer.sendmailtask.mail.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f35ec3ad66199e6c13c648c9a2208f5bf88f439a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293934"
---
# <a name="send-mail-task"></a>傳送郵件工作

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  傳送郵件工作會傳送電子郵件訊息。 藉由使用傳送郵件工作，封裝即可在封裝工作流程中的工作成功或失敗時傳送訊息，或傳送回應封裝在執行階段所引發事件的訊息。 例如，工作可通知資料庫管理員「備份資料庫」工作成功或失敗。  
  
 您可以利用下列方式設定傳送郵件工作：  
  
-   提供電子郵件訊息的訊息文字。  
  
-   提供電子郵件訊息的主旨。  
  
-   設定訊息的優先順序等級。 這項工作支援三種優先順序等級：一般、低和高。  
  
-   指定 [收件者]、[副本] 和 [密件副本] 欄位的收件者。 如果工作指定多位收件者，則會以分號分隔各收件者。  
  
    > [!NOTE]  
    >  根據網際網路標準，[收件者]、[副本] 和 [密件副本] 欄位限制為 256 個字元。  
  
-   包含附加檔案。 如果工作指定多個附加檔案，則會以縱線 (|) 字元分隔各附加檔案。  
  
    > [!NOTE]  
    >  如果封裝執行時附加檔案不存在，則會發生錯誤。  
  
-   指定要使用的 SMTP 連接管理員。  
  
    > [!IMPORTANT]  
    >  SMTP 連接管理員僅支援匿名驗證和 Windows 驗證， 而不支援基本驗證。  
  
 訊息文字可以是您提供的字串、包含文字的檔案連接，或包含文字的變數名稱。 工作會使用「檔案」連接管理員連接檔案。 如需相關資訊，請參閱 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
 工作會使用 SMTP 連接管理員連接到郵件伺服器。 如需相關資訊，請參閱 [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md)。  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>傳送郵件工作上可用的自訂記錄訊息  
 下表列出「傳送郵件」工作的自訂記錄項目。 如需詳細資訊，請參閱 [集成服務 &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|Description|  
|---------------|-----------------|  
|**SendMailTaskBegin**|指出工作已經開始傳送電子郵件訊息。|  
|**SendMailTaskEnd**|指出工作已經完成傳送電子郵件訊息。|  
|**SendMailTaskInfo**|提供有關工作的描述性資訊。|  
  
## <a name="configuring-the-send-mail-task"></a>設定傳送郵件工作  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列主題：  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何以程式設計方式設定這些屬性的詳細資訊，請按以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>相關工作  
 如需如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定這些屬性的資訊，請按一下 [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)。  
  
## <a name="related-content"></a>相關內容  
  
-   shareourideas.com 上的技術文件： [如何在 C# 中傳送包含傳遞通知的電子郵件](https://go.microsoft.com/fwlink/?LinkId=237625)(如何在 C# 中傳送包含傳遞通知的電子郵件)  
  
## <a name="send-mail-task-editor-general-page"></a>傳送郵件工作編輯器 (一般頁面)
  使用 [傳送郵件工作編輯器]  對話方塊的 [一般]  頁面，即可命名和描述傳送郵件工作。  
  
### <a name="options"></a>選項。  
 **名稱**  
 為傳送郵件工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
 **注意** ：工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入傳送郵件工作的描述。  
  
## <a name="send-mail-task-editor-mail-page"></a>傳送郵件工作編輯器 (郵件頁面)
  使用 [傳送郵件工作編輯器]  對話方塊的 [郵件]  頁面，即可指定收件者、訊息類型以及訊息的優先權。 您也可以附加檔案至訊息。 訊息文字可以是您提供的字串、包含文字之檔案的檔案連接，或包含文字之變數的名稱。  
  
### <a name="options"></a>選項。  
 **SMTPConnection**  
 在清單中選取 SMTP 連線管理員，或按一下 [\<新增連線...>]  ，即可建立新的連線管理員。  
  
> [!IMPORTANT]  
>  SMTP 連接管理員僅支援匿名驗證和 Windows 驗證， 而不支援基本驗證。  
  
 **相關主題：** [SMTP 連線管理員](../../integration-services/connection-manager/smtp-connection-manager.md)  
  
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
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接輸入**|將來源設定為訊息文字。 選取此值會顯示動態選項 [MessageSource]  。|  
|**檔案連接**|將來源設定為包含訊息文字的檔案。 選取此值會顯示動態選項 [MessageSource]  。|  
|**變數**|將來源設定為包含訊息文字的變數。 選取此值會顯示動態選項 [MessageSource]  。|  
  
 **優先權**  
 設定訊息的優先權。  
  
 **附加檔案**  
 提供電子郵件訊息之附加檔案的檔案名稱，以垂直線 (|) 字元分隔。  
  
> [!NOTE]  
>  根據網際網路標準，[收件者]、[副本] 和 [密件副本] 欄位限制為 256 個字元。  
  
### <a name="messagesourcetype-dynamic-options"></a>MessageSourceType 動態選項  
  
#### <a name="messagesourcetype--direct-input"></a>MessageSourceType = 直接輸入  
 **MessageSource**  
 輸入訊息文字或按一下瀏覽按鈕 ([...])，然後在 [訊息來源]  對話方塊中輸入訊息。  
  
#### <a name="messagesourcetype--file-connection"></a>MessageSourceType = 檔案連接  
 **MessageSource**  
 在清單中選取檔案連線管理員，或按一下 [\<新增連線...>]  ，即可建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="messagesourcetype--variable"></a>MessageSourceType = 變數  
 **MessageSource**  
 在清單中選取變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[新增變數](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
