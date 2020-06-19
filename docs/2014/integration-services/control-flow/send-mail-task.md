---
title: 傳送電子郵件工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sendmailtask.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 701416b401d428cda9fe0e78b9219dfb2ef53167
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84918208"
---
# <a name="send-mail-task"></a>傳送郵件工作
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
  
 訊息文字可以是您提供的字串、包含文字的檔案連接，或包含文字的變數名稱。 工作會使用「檔案」連接管理員連接檔案。 如需相關資訊，請參閱 [Flat File Connection Manager](../connection-manager/file-connection-manager.md)。  
  
 工作會使用 SMTP 連接管理員連接到郵件伺服器。 如需相關資訊，請參閱 [SMTP Connection Manager](../connection-manager/smtp-connection-manager.md)。  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>傳送郵件工作上可用的自訂記錄訊息  
 下表列出「傳送郵件」工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)和[自訂訊息以進行記錄](../custom-messages-for-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`SendMailTaskBegin`|指出工作已經開始傳送電子郵件訊息。|  
|`SendMailTaskEnd`|指出工作已經完成傳送電子郵件訊息。|  
|`SendMailTaskInfo`|提供有關工作的描述性資訊。|  
  
## <a name="configuring-the-send-mail-task"></a>設定傳送郵件工作  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [傳送郵件工作編輯器 &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [傳送郵件工作編輯器 &#40;郵件頁面&#41;](../send-mail-task-editor-mail-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關如何以程式設計方式設定這些屬性的詳細資訊，請按以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>相關工作  
 如需如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定這些屬性的資訊，請按一下 [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)。  
  
## <a name="related-content"></a>相關內容  
  
-   shareourideas.com 上的技術文件： [如何在 C# 中傳送包含傳遞通知的電子郵件](https://go.microsoft.com/fwlink/?LinkId=237625)(如何在 C# 中傳送包含傳遞通知的電子郵件)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](integration-services-tasks.md)   
 [控制流程](control-flow.md)  
  
  
