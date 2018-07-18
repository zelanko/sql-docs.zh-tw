---
title: 傳送作業工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferjobstask.f1
- sql13.dts.designer.transferjobstask.general.f1
- sql13.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0c06201f3c1512fb45f249983b24a275aaff4377
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35409600"
---
# <a name="transfer-jobs-task"></a>傳送作業工作
  「傳送作業」工作會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之間，傳送一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 作業。  
  
 「傳送作業」工作可以設定為傳送所有作業，或只傳送指定的作業。 您還可以指出是否在目的地啟用已傳送的作業。  
  
 要傳送的作業可能已存在於目的地上。 可以設定「傳送作業」工作以下列方式處理現有的作業：  
  
-   覆寫現有的作業。  
  
-   存在重複的作業時讓工作失敗。  
  
-   略過重複的作業。  
  
 在執行階段，「傳送作業」工作會使用一或兩個 SMO 連接管理員，連接到來源和目的地伺服器。 SMO 連接管理員會在「傳送作業」工作以外另行設定，然後在「傳送作業」工作中參考。 存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需詳細資訊，請參閱 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
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
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列主題：  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-jobs-task-editor-general-page"></a>傳送作業工作編輯器 (一般頁面)
  使用 **[傳送作業工作編輯器]** 對話方塊的 **[一般]** 頁面，即可命名和描述傳送作業工作。  
  
> [!NOTE]  
>  只有目的地伺服器上的 **系統管理員 (sysadmin)** 固定伺服器角色的成員，或其中一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色的成員，才能在目的地伺服器上成功建立作業。 若要存取來源伺服器上的作業，則在來源伺服器上使用者必須至少是 **SQLAgentUserRole** 固定資料庫角色的成員。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色及其權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
### <a name="options"></a>選項。  
 **名稱**  
 輸入傳送作業工作的唯一名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入傳送作業工作的描述。  
  
## <a name="transfer-jobs-task-editor-jobs-page"></a>傳送作業工作編輯器 (作業頁面)
  使用 [傳送作業工作編輯器] 對話方塊的 [作業] 頁面，即可指定屬性用來將一或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一個執行個體複製到另一個。  
  
> [!NOTE]  
>  若要存取來源伺服器上的作業，使用者就必須至少是伺服器上之 **SQLAgentUserRole** 固定資料庫角色的成員。 若要在目的地伺服器上順利建立作業，使用者就必須是 **sysadmin** 固定伺服器角色的成員，或是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色的成員。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色及其權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
### <a name="options"></a>選項。  
 **SourceConnection**  
 在清單中選取 SMO 連線管理員，或按一下 [\<新增連線...>] 建立來源伺服器的新連線。  
  
 **DestinationConnection**  
 在清單中選取一個 SMO 連線管理員，或按一下 [\<新增連線...>]，以建立目的地伺服器的新連線。  
  
 **TransferAllJobs**  
 選取工作是否應將所有作業或只有指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，從來源複製到目的地伺服器。  
  
 此屬性具有下表所列的選項：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**True**|複製所有作業。|  
|**False**|只複製指定的作業。|  
  
 **JobsList**  
 按一下瀏覽按鈕 **(…)** 來選取要複製的作業。 必須至少選取一個作業。  
  
> [!NOTE]  
>  選取要複製的作業之前，請指定 **SourceConnection** 。  
  
 當 **TransferAllJobs** 設定為 **True** 時，無法使用 **JobsList**選項。  
  
 **IfObjectExists**  
 選取工作應如何處理已經存在於目的地伺服器上，且具有相同名稱的作業。  
  
 此屬性具有下表所列的選項：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**FailTask**|如果具有相同名稱的作業己經存在於目的地伺服器上，工作就會失敗。|  
|**Overwrite**|工作會覆寫目的地伺服器上具有相同名稱的作業。|  
|**Skip**|工作會略過存在於目的地伺服器上具有相同名稱的作業。|  
  
 **EnableJobsAtDestination**  
 選取是否應啟用已複製到目的地伺服器的作業。  
  
 此屬性具有下表所列的選項：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**True**|啟用目的地伺服器上的作業。|  
|**False**|停用目的地伺服器上的作業。|  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
