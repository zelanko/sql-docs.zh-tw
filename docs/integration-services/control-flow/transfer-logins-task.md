---
title: "傳送登入工作 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferloginstask.f1
- sql13.dts.designer.transferloginstask.general.f1
- sql13.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins task [Integration Services]
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e62891da63a881b525067dbb3afba820eed24b26
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="transfer-logins-task"></a>傳送登入工作
  「傳送登入」工作會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體之間傳送一個或多個登入。  
  
## <a name="transfer-logins-between-instances-of-sql-server"></a>在 SQL Server 的執行個體之間傳送登入  
 傳送登入工作支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來源和目的地。  
  
## <a name="events"></a>事件  
 「傳送登入」工作會引發報告已傳送登入數目的資訊事件，並在覆寫登入時引發警告事件。  
  
 該工作並不報告登入傳送的累加進度，它只報告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>執行值  
 工作之 **ExecutionValue** 屬性中定義的執行值會傳回已傳送的登入數目。 透過將使用者定義變數指派給「傳送登入」工作的 **ExecValueVariable** 屬性，可將與登入傳送相關的資訊用於封裝中的其他物件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="log-entries"></a>記錄項目  
 「傳送登入」工作包含下列自訂記錄項目：  
  
-   TransferLoginsTaskStarTransferringObjects   此記錄項目報告傳送已開始。 記錄項目會包含開始時間。  
  
-   TransferLoginsTaskFinishedTransferringObjects   此記錄項目報告傳送已完成。 記錄項目會包含結束時間。  
  
 此外， **OnInformation** 事件的記錄項目會報告已傳送的登入數目，並會為在目的地上覆寫的每個登入，寫入 **OnWarning** 事件的記錄項目。  
  
## <a name="security-and-permissions"></a>安全性和權限  
 若要瀏覽來源伺服器上的登入，並在目的地伺服器上建立登入，使用者必須同時是兩個伺服器上 sysadmin 伺服器角色的成員。  
  
## <a name="configuration-of-the-transfer-logins-task"></a>設定傳送登入工作  
 「傳送登入」工作可以設定為傳送所有登入、只傳送指定的登入，或只傳送具有指定之資料庫存取權的所有登入。 無法傳送 sa 登入。 可能已重新命名 SA 登入，不過，重新命名的 SA 登入仍然無法傳送。  
  
 您還可以指出工作是否複製與登入相關聯的安全性識別碼 (SID)。 如果將「傳送登入」工作與「傳送資料庫」工作一起使用，則必須將 SID 複製到目的地，否則，目的地資料庫將無法辨識傳送的登入。  
  
 在目的地上，會停用傳送的登入，並為其指派隨機密碼。 目的地伺服器上 sysadmin 角色的成員必須變更密碼，並啟用登入，才可以使用這些登入。  
  
 要傳送的登入可能已存在於目的地上。 可以設定「傳送登入」工作以下列方式處理現有的登入：  
  
-   覆寫現有的登入。  
  
-   存在重複的登入時讓工作失敗。  
  
-   略過重複的登入。  
  
 在執行階段，「傳送登入」工作會使用兩個 SMO 連接管理員，連接到來源和目的地伺服器。 SMO 連接管理員會在「傳送登入」工作以外另行設定，然後在「傳送登入」工作中參考。 存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需詳細資訊，請參閱 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-logins-task"></a>以程式設計方式設定傳送登入工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
## <a name="transfer-logins-task-editor-general-page"></a>傳送登入工作編輯器 (一般頁面)
  使用 **[傳送登入工作編輯器]** 對話方塊的 **[一般]** 頁面，即可命名和描述傳送登入工作。  
  
### <a name="options"></a>選項。  
 **名稱**  
 輸入傳送登入工作的唯一名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入傳送登入工作的描述。  
  
## <a name="transfer-logins-task-editor-logins-page"></a>傳送登入工作編輯器 (登入頁面)
  使用 [傳送登入工作編輯器] 對話方塊的 [登入] 頁面，即可指定屬性將一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一個執行個體複製到另一個執行個體。  
  
> [!IMPORTANT]  
>  執行傳送登入工作時，目的地伺服器上會建立具隨機密碼的登入，且會停用這些密碼。 若要使用這些登入， **系統管理員** 固定伺服器角色的成員就必須變更密碼，然後啟用密碼。 無法傳送 **sa** 登入。  
  
### <a name="options"></a>選項。  
 **SourceConnection**  
 在清單中選取 SMO 連線管理員，或按一下 [\<新增連線...>] 建立來源伺服器的新連線。  
  
 **DestinationConnection**  
 在清單中選取一個 SMO 連線管理員，或按一下 [\<新增連線...>]，以建立目的地伺服器的新連線。  
  
 **LoginsToTransfer**  
 選取要從來源複製到目的地伺服器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 此屬性具有下表所列的選項：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**AllLogins**|來源伺服器上的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，都會複製到目的地伺服器。|  
|**SelectedLogins**|只有使用 **LoginsList** 指定的登入，才會複製到目的地伺服器。|  
|**AllLoginsFromSelectedDatabases**|使用 **DatabasesList** 指定之資料庫中的所有登入，都會複製到目的地伺服器。|  
  
 **LoginsList**  
 選取來源伺服器上要複製到目的地伺服器的登入。 唯有針對 [LoginsToTransfer] 選取了 [SelectedLogins] 時，才能使用此選項。  
  
 **DatabasesList**  
 選取來源伺服器上的資料庫，其中包含要複製到目的地伺服器的登入。 唯有針對 [LoginsToTransfer] 選取了 [AllLoginsFromSelectedDatabases] 時，才能使用此選項。  
  
 **IfObjectExists**  
 選取工作應如何處理已經存在於目的地伺服器上，且具有相同名稱的登入。  
  
 此屬性具有下表所列的選項：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**FailTask**|如果具有相同名稱的登入已經存在於目的地伺服器上，工作就會失敗。|  
|**Overwrite**|工作會覆寫目的地伺服器上具有相同名稱的登入。|  
|**Skip**|工作會略過目的地伺服器上具有相同名稱的登入。|  
  
 **CopySids**  
 選取與登入相關聯的安全性識別碼，是否應複製到目的地伺服器。 如果「傳送登入」工作是與「傳送資料庫」工作一併使用，[CopySids] 就必須設定為 [True]。 否則，已傳送的資料庫就無法辨識被複製的登入。  
  
