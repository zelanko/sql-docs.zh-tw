---
title: "傳送郵件工作 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sendmailtask.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: fd6f7a19c1b553ee06013a4a24fbbf26a759a6cd
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

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
  
 訊息文字可以是您提供的字串、包含文字的檔案連接，或包含文字的變數名稱。 工作會使用「檔案」連接管理員連接檔案。 如需相關資訊，請參閱 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
 工作會使用 SMTP 連接管理員連接到郵件伺服器。 如需相關資訊，請參閱 [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md)。  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>傳送郵件工作上可用的自訂記錄訊息  
 下表列出「傳送郵件」工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**SendMailTaskBegin**|指出工作已經開始傳送電子郵件訊息。|  
|**SendMailTaskEnd**|指出工作已經完成傳送電子郵件訊息。|  
|**SendMailTaskInfo**|提供有關工作的描述性資訊。|  
  
## <a name="configuring-the-send-mail-task"></a>設定傳送郵件工作  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [傳送郵件工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/send-mail-task-editor-general-page.md)  
  
-   [傳送郵件工作編輯器 &#40;郵件頁面&#41;](../../integration-services/control-flow/send-mail-task-editor-mail-page.md)  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何以程式設計方式設定這些屬性的詳細資訊，請按以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>相關工作  
 如需如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定這些屬性的資訊，請按一下 [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)。  
  
## <a name="related-content"></a>相關內容  
  
-   shareourideas.com 上的技術文章： [How to send email with delivery notification in C#](http://go.microsoft.com/fwlink/?LinkId=237625)  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
