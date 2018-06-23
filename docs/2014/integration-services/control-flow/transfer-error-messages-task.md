---
title: 傳送錯誤訊息工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.transfererrormessagestask.f1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e6d8bc72c3c713dc1a113490431f4dba81c2a11a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131773"
---
# <a name="transfer-error-messages-task"></a>傳送錯誤訊息工作
  [傳送錯誤訊息] 工作會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之間傳送一或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者自訂的錯誤訊息。 使用者定義的訊息是識別碼等於或大於 50000 的訊息。 識別碼小於 50000 的訊息是系統錯誤訊息，這種訊息無法使用「傳送錯誤訊息」工作進行傳送。  
  
 「傳送錯誤訊息」工作可以設定為傳送所有錯誤訊息，或只傳送指定的錯誤訊息。 使用者自訂的錯誤訊息可能有很多不同的語言版本，您可以設定工作只傳送所選語言的訊息。 在您可以傳送其他語言版本的訊息至目的地伺服器之前，使用字碼頁 1033 的 us_english 版訊息必須存在於該伺服器上。  
  
 master 資料庫中的 sysmessages 資料表包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的所有錯誤訊息 (包括系統和使用者定義的訊息)。  
  
 要傳送的使用者自訂訊息可能已存在於目的地上。 如果識別碼和語言相同，則會將錯誤訊息定義為重複錯誤訊息。 可以設定「傳送錯誤訊息」工作以下列方式處理現有的錯誤訊息：  
  
-   覆寫現有的錯誤訊息。  
  
-   存在重複的訊息時讓工作失敗。  
  
-   略過重複的錯誤訊息。  
  
 在執行階段，「傳送錯誤訊息」工作會使用一或多個 SMO 連接管理員，連接到來源和目的地伺服器。 SMO 連接管理員會在「傳送錯誤訊息」工作以外另行設定，然後在「傳送錯誤訊息」工作中參考。 存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需詳細資訊，請參閱 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)。  
  
 [傳送錯誤訊息] 工作支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來源和目的地。 將哪一個用作來源或目的地是沒有限制的。  
  
## <a name="events"></a>事件  
 「傳送錯誤訊息」工作會引發報告已傳送錯誤訊息數目的資訊事件。  
  
 該工作並不報告錯誤訊息傳送的累加進度，它只報告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>執行值  
 工作之 `ExecutionValue` 屬性中定義的執行值會傳回已傳送的錯誤訊息數目。 藉由指定使用者定義變數，以`ExecValueVariable`屬性 「 傳送錯誤訊息 」 工作的錯誤訊息傳送相關的資訊可供其他物件中封裝。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)和[在封裝中使用變數](../use-variables-in-packages.md)。  
  
## <a name="log-entries"></a>記錄項目  
 「傳送錯誤訊息」工作包含下列自訂記錄項目：  
  
-   TransferErrorMessagesTaskStartTransferringObjects    此記錄項目報告傳送已開始。 記錄項目會包含開始時間。  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects   此記錄項目報告傳送已完成。 記錄項目會包含結束時間。  
  
 此外，記錄項目`OnInformation`事件是用以報告已傳送的錯誤訊息和記錄項目數目`OnWarning event`寫入每個錯誤訊息會覆寫目的地上。  
  
## <a name="security-and-permissions"></a>安全性和權限  
 若要建立新的錯誤訊息，執行封裝的使用者必須是目的地伺服器上 sysadmin 或 serveradmin 伺服器角色的成員。  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>傳送錯誤訊息工作的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [傳送錯誤訊息工作編輯器&#40;[一般] 頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [傳送錯誤訊息工作編輯器&#40;郵件頁面&#41;](../transfer-error-messages-task-editor-messages-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關如何以程式設計方式設定這些屬性的詳細資訊，請按以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](integration-services-tasks.md)   
 [控制流程](control-flow.md)  
  
  