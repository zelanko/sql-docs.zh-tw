---
title: "傳送作業工作 |Microsoft 文件"
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
- sql13.dts.designer.transferjobstask.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 61839f15a36ff679f4edfc4585192100c370bb43
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-jobs-task"></a>傳送作業工作
  「傳送作業」工作會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之間，傳送一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 作業。  
  
 「傳送作業」工作可以設定為傳送所有作業，或只傳送指定的作業。 您還可以指出是否在目的地啟用已傳送的作業。  
  
 要傳送的作業可能已存在於目的地上。 可以設定「傳送作業」工作以下列方式處理現有的作業：  
  
-   覆寫現有的作業。  
  
-   存在重複的作業時讓工作失敗。  
  
-   略過重複的作業。  
  
 在執行階段，「傳送作業」工作會使用一或兩個 SMO 連接管理員，連接到來源和目的地伺服器。 SMO 連接管理員會在「傳送作業」工作以外另行設定，然後在「傳送作業」工作中參考。 存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需相關資訊，請參閱 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>在 SQL Server 的執行個體之間傳送作業  
 「傳送作業」工作支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來源和目的地。 將哪一個用作來源或目的地是沒有限制的。  
  
## <a name="events"></a>事件  
 「傳送作業」工作會引發報告已傳送作業數目的資訊事件，並在覆寫作業時引發警告事件。 該工作並不報告作業傳送的累加進度，它只報告 0% 和 100% 完成。  
  
## <a name="execution-value"></a>執行值  
 工作之 **ExecutionValue** 屬性中定義的執行值會傳回已傳送的作業數目。 透過將使用者定義變數指派給「傳送作業」工作的 **ExecValueVariable** 屬性，可將與作業傳送相關的資訊用於封裝中的其他物件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="log-entries"></a>記錄項目  
 「傳送作業」工作包含下列自訂記錄項目：  
  
-   TransferJobsTaskStarTransferringObjects   此記錄項目報告傳送已開始。 記錄項目會包含開始時間。  
  
-   TransferJobsTaskFinishedTransferringObjects   此記錄項目報告傳送已完成。 記錄項目會包含結束時間。  
  
 此外， **OnInformation** 事件的記錄項目會報告已傳送的作業數目，並會為在目的地上覆寫的每個作業，寫入 **OnWarning** 事件的記錄項目。  
  
## <a name="security-and-permissions"></a>安全性和權限  
 若要傳送作業，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的來源和目的地執行個體上，使用者都必須是系統管理員 (sysadmin) 固定伺服器角色的成員，或者是 msdb 資料庫上固定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 固定資料庫角色的其中一個成員。  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>設定傳送作業工作  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [傳送作業工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/transfer-jobs-task-editor-general-page.md)  
  
-   [傳送作業工作編輯器 &#40;作業頁面&#41;](../../integration-services/control-flow/transfer-jobs-task-editor-jobs-page.md)  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
