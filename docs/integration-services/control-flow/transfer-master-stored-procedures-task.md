---
title: 傳送主要預存程序工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfermasterspstask.f1
- sql13.dts.designer.transferstoredprocedurestask.general.f1
- sql13.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fc3b10cd913f0cf2d270fd228ad4729f12ec0f53
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916084"
---
# <a name="transfer-master-stored-procedures-task"></a>傳送主要預存程序工作

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  「傳送主要預存程序」工作會在 **執行個體上的** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫之間，傳送一個或多個使用者自訂預存程序。 若要從 **master** 資料庫傳送預存程序，程序的擁有者必須為 dbo。  
  
 可以設定「傳送主要預存程序」工作傳送所有的預存程序，或只傳送指定的預存程序。 此工作不會複製系統預存程序。  
  
 目的地可能已存在要傳送的主要預存程序。 可以設定「傳送主要預存程序」工作以下列方式處理現有的預存程序：  
  
-   覆寫現有預存程序。  
  
-   存在重複的預存程序時讓工作失敗。  
  
-   略過重複的預存程序。  
  
 在執行階段，「傳送主要預存程序」工作會使用兩個 SMO 連接管理員，連接到來源和目的地伺服器。 SMO 連結管理員會在「傳送主要預存程序」工作以外另行設定，然後在「傳送主要預存程序」工作中參考。 存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需詳細資訊，請參閱 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
## <a name="transferring-stored-procedures-between-instances-of-sql-server"></a>在 SQL Server 的執行個體之間傳送預存程序  
 「傳送主要預存程序」工作可支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來源及目的地。  
  
## <a name="events"></a>事件  
 該工作會引發報告已傳送預存程序數目的資訊事件，並在覆寫預存程序時引發警告事件。  
  
 「傳送主要預存程序」工作並不報告登入傳送的累加進度，它只報告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>執行值  
 工作之 **ExecutionValue** 屬性中定義的執行值會傳回已傳送的預存程序數。 透過將使用者自訂變數指派給「傳送主要預存程序」工作的 **ExecValueVariable** 屬性，可將與預存程序傳送相關的資訊用於封裝中的其他物件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="log-entries"></a>記錄項目  
 「傳送主要預存程序」工作包含下列自訂記錄項目：  
  
-   TransferStoredProceduresTaskStartTransferringObjects  此記錄項目報告傳送已開始。 記錄項目會包含開始時間。  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  此記錄項目報告傳送已完成。 記錄項目會包含結束時間。  
  
 此外， **OnInformation** 事件的記錄項目會報告已傳送的預存程序數目，並會為在目的地上覆寫的每個預存程序，寫入 **OnWarning** 事件的記錄項目。  
  
## <a name="security-and-permissions"></a>安全性和權限  
 使用者必須具有來源上 **master** 資料庫中預存程序清單的檢視權限，且必須是系統管理員 (sysadmin) 伺服器角色的成員，或者具有目的地伺服器上 **master** 資料庫中已建立之預存程序的權限。  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>設定傳送主要預存程序工作  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列主題：  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何以程式設計方式設定這些屬性的詳細資訊，請按以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>以程式設計方式設定傳送主要預存程序工作  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-master-stored-procedures-task-editor-general-page"></a>傳送主要預存程序工作編輯器 (一般頁面)
  使用 [傳送主要預存程序工作編輯器] 對話方塊的 [一般] 頁面，即可命名和描述傳送主要預存程序工作。  
  
> [!NOTE]  
>  此工作只會從來源伺服器上的 **master** 資料庫，將 **dbo** 擁有的使用者定義預存程序，傳送到目的地伺服器上的 **master** 資料庫。 使用者必須有目的地伺服器上之 **master** 資料庫的 CREATE PROCEDURE 權限，或是目的地伺服器上之 **sysadmin** 固定伺服器角色的成員，才能在目的地伺服器建立預存程序。  
  
### <a name="options"></a>選項。  
 **名稱**  
 輸入傳送主要預存程序工作的唯一名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入傳送主要預存程序工作的描述。  
  
## <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>傳送主要預存程序工作編輯器 (預存程序頁面)
  使用 [傳送主要預存程序工作編輯器] 對話方塊的 [預存程序] 頁面，即可指定屬性，以將一個或多個使用者定義預存程序從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之某個執行個體的 **master** 資料庫，複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之另一個執行個體的 **master** 資料庫中。  
  
> [!NOTE]  
>  此工作只會從來源伺服器上的 **master** 資料庫，將 **dbo** 擁有的使用者定義預存程序，傳送到目的地伺服器上的 **master** 資料庫。 使用者必須有目的地伺服器上之 **master** 資料庫的 CREATE PROCEDURE 權限，或是目的地伺服器上之 **sysadmin** 固定伺服器角色的成員，才能在目的地伺服器建立預存程序。  
  
### <a name="options"></a>選項。  
 **SourceConnection**  
 在清單中選取一個 SMO 連線管理員，或按一下 **\<New connection...>** ，以建立新的來源伺服器連線。  
  
 **DestinationConnection**  
 在清單中選取一個 SMO 連線管理員，或按一下 **\<New connection...>** ，以建立新的目的地伺服器連線。  
  
 **IfObjectExists**  
 選取工作應如何處理在目的地伺服器上的 **master** 資料庫中已經存在有相同名稱的使用者定義預存程序。  
  
 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**FailTask**|如果目的地伺服器上的 **master** 資料庫中已經存在有相同名稱的預存程序，則工作失敗。|  
|**Overwrite**|工作會覆寫目的地伺服器上的 **master** 資料庫中有相同名稱的預存程序。|  
|**Skip**|工作會略過目的地伺服器上的 **master** 資料庫中存在有相同名稱的預存程序。|  
  
 **TransferAllStoredProcedures**  
 選取是否應將來源伺服器上之 **master** 資料庫中的所有使用者定義預存程序，複製到目的地伺服器。  
  
|值|描述|  
|-----------|-----------------|  
|**True**|複製 **master** 資料庫中的所有使用者定義預存程序。|  
|**False**|只複製指定的預存程序。|  
  
 **StoredProceduresList**  
 選取應將來源伺服器上之 **master** 資料庫中的哪些使用者定義預存程序，複製到目的地 **master** 資料庫。 只有 [TransferAllStoredProcedures]  設定為 [False]  時，才能使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [傳送 SQL Server 物件工作](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
