---
title: "傳送錯誤訊息工作 |Microsoft 文件"
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
- sql13.dts.designer.transfererrormessagestask.f1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3f13e3e6e22e2b4f3b74c80a249a098d93ad5b9f
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-error-messages-task"></a>傳送錯誤訊息工作
  [傳送錯誤訊息] 工作會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之間傳送一或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者自訂的錯誤訊息。 使用者定義的訊息是識別碼等於或大於 50000 的訊息。 識別碼小於 50000 的訊息是系統錯誤訊息，這種訊息無法使用「傳送錯誤訊息」工作進行傳送。  
  
 「傳送錯誤訊息」工作可以設定為傳送所有錯誤訊息，或只傳送指定的錯誤訊息。 使用者自訂的錯誤訊息可能有很多不同的語言版本，您可以設定工作只傳送所選語言的訊息。 在您可以傳送其他語言版本的訊息至目的地伺服器之前，使用字碼頁 1033 的 us_english 版訊息必須存在於該伺服器上。  
  
 master 資料庫中的 sysmessages 資料表包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的所有錯誤訊息 (包括系統和使用者定義的訊息)。  
  
 要傳送的使用者自訂訊息可能已存在於目的地上。 如果識別碼和語言相同，則會將錯誤訊息定義為重複錯誤訊息。 可以設定「傳送錯誤訊息」工作以下列方式處理現有的錯誤訊息：  
  
-   覆寫現有的錯誤訊息。  
  
-   存在重複的訊息時讓工作失敗。  
  
-   略過重複的錯誤訊息。  
  
 在執行階段，「傳送錯誤訊息」工作會使用一或多個 SMO 連接管理員，連接到來源和目的地伺服器。 SMO 連接管理員會在「傳送錯誤訊息」工作以外另行設定，然後在「傳送錯誤訊息」工作中參考。 存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需相關資訊，請參閱 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
 [傳送錯誤訊息] 工作支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來源和目的地。 將哪一個用作來源或目的地是沒有限制的。  
  
## <a name="events"></a>事件  
 「傳送錯誤訊息」工作會引發報告已傳送錯誤訊息數目的資訊事件。  
  
 該工作並不報告錯誤訊息傳送的累加進度，它只報告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>執行值  
 工作之 **ExecutionValue** 屬性中定義的執行值會傳回已傳送的錯誤訊息數目。 透過將使用者定義的變數指派給 [傳送錯誤訊息] 工作的 **ExecValueVariable** 屬性，可將與錯誤訊息傳送相關的資訊用於封裝中的其他物件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="log-entries"></a>記錄項目  
 「傳送錯誤訊息」工作包含下列自訂記錄項目：  
  
-   TransferErrorMessagesTaskStartTransferringObjects    此記錄項目報告傳送已開始。 記錄項目會包含開始時間。  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects   此記錄項目報告傳送已完成。 記錄項目會包含結束時間。  
  
 此外， **OnInformation** 事件的記錄項目會報告已傳送的錯誤訊息，並會為在目的地上覆寫的每個錯誤訊息，寫入 [OnWarning 事件] 的記錄項目。  
  
## <a name="security-and-permissions"></a>安全性和權限  
 若要建立新的錯誤訊息，執行封裝的使用者必須是目的地伺服器上 sysadmin 或 serveradmin 伺服器角色的成員。  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>傳送錯誤訊息工作的組態  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [傳送錯誤訊息工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/transfer-error-messages-task-editor-general-page.md)  
  
-   [傳送錯誤訊息工作編輯器 &#40;訊息頁面&#41;](../../integration-services/control-flow/transfer-error-messages-task-editor-messages-page.md)  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何以程式設計方式設定這些屬性的詳細資訊，請按以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
