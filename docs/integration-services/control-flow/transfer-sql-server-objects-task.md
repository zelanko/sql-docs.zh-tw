---
description: 傳送 SQL Server 物件工作
title: 傳送 SQL Server 物件工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfersqlserverobjectstask.f1
- sql13.dts.designer.transfersqlserverobjects.general.f1
- sql13.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2cd15daac2c287c2dc750e1f79032f855d5640d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88349164"
---
# <a name="transfer-sql-server-objects-task"></a>傳送 SQL Server 物件工作

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間，傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫中的一個或多個類型物件。 例如，該工作可以複製資料表和預存程序。 因用作來源的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本不同，可複製不同類型的物件。 例如，只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫包含結構描述和使用者定義彙總。  
  
## <a name="objects-to-transfer"></a>要傳送的物件  
 可以複製指定資料庫中的伺服器角色、角色和使用者，也可以複製所傳送物件的權限。 透過將相關聯的使用者、角色和權限與物件一起複製，可以讓所傳送物件立即可以在目的地伺服器上進行運作。  
  
 下表列出可複製的物件類型。  
  
|Object|  
|------------|  
|資料表|  
|檢視|  
|預存程序|  
|使用者定義的函式|  
|Defaults|  
|使用者自訂資料類型|  
|資料分割函數|  
|資料分割配置|  
|結構描述|  
|組件|  
|使用者定義彙總|  
|使用者定義類型|  
|XML 結構描述集合|  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之執行個體中建立的使用者定義類型 (UDT) 相依於 Common Language Runtime (CLR) 組件。 如果使用「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作傳送 UDT，您也必須設定該工作以傳送相依物件。 若要傳送相依物件，請將 **IncludeDependentObjects** 屬性設定為 **True**。  
  
### <a name="table-options"></a>資料表選項  
 複製資料表時，您可以指出要在複製處理中包含之資料表相關項目的類型。 您可以在複製相關資料表時一併複製下列類型的項目：  
  
-   索引  
  
-   觸發程序  
  
-   全文檢索索引  
  
-   主索引鍵  
  
-   外部索引鍵  
  
 您還可以指出工作所產生的指令碼是否為 Unicode 格式。  
  
## <a name="destination-options"></a>目的地選項  
 您可以設定「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作在傳送中包含結構描述名稱、資料、所傳送物件的擴充屬性和相依物件。 如果複製資料，則它可以取代或附加現有資料。  
  
 部分選項只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 例如，僅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援結構描述。  
  
## <a name="security-options"></a>安全性選項  
 「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作可以包含來源的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫層級使用者和角色、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，以及所傳送物件的權限。 例如，傳送可以包含所傳送資料表的權限。  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>在 SQL Server 的執行個體之間傳送物件  
 「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作可支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的來源和目的地。  
  
## <a name="events"></a>事件  
 該工作會引發報告已傳送物件的資訊事件，並在覆寫物件時引發警告事件。 還會為動作 (例如，截斷資料庫資料表) 引發資訊事件。  
  
 「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作並不報告物件傳送的累加進度，它只報告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>執行值  
 工作之 **ExecutionValue** 屬性中儲存的執行值會傳回已傳送的物件數目。 透過將使用者定義變數指派給「傳送 SQL Server 物件」工作的 **ExecValueVariable** 屬性，可將與物件傳送相關的資訊用於封裝中的其他物件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="log-entries"></a>記錄項目  
 「傳送 SQL Server 物件」工作包含下列自訂記錄項目：  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects：此記錄項目報告傳送已開始。 記錄項目會包含開始時間。  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects：此記錄項目報告傳送已完成。 記錄項目會包含結束時間。  
  
 此外， **OnInformation** 事件的記錄項目會報告已為傳送選取之物件類型的物件數目、已傳送的物件數目，以及動作 (例如，隨資料表一同傳送資料時截斷資料表)。 為在目的地上覆寫的每個物件寫入 **OnWarning** 事件的記錄項目。  
  
## <a name="security-and-permissions"></a>安全性和權限  
 使用者必須具有在來源伺服器上瀏覽物件的權限，且必須具有在目的地伺服器上卸除和建立物件的權限，此外，使用者還必須能夠存取指定的資料庫和資料庫物件。  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>設定傳送 SQL Server 物件工作  
 可以設定「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作傳送所有物件、同一類型的所有物件，或只傳送同一類型的指定物件。 例如，您可以選擇只複製 AdventureWorks 資料庫中已選取的資料表。  
  
 如果「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作傳送資料表，則您可指定要隨該資料表一同複製之資料表相關物件的類型。 例如，您可以指定隨資料表一同複製的主索引鍵。  
  
 若要進一步加強所傳送物件的功能，您可以設定「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作在傳送中包含結構描述名稱、資料、所傳送物件的擴充屬性和相依物件。 複製資料時，您可以指定是取代還是附加現有資料。  
  
 在執行階段，「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作會使用兩個 SMO 連線管理員，連接到來源和目的地伺服器。 SMO 連接管理員會在「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作以外另行設定，然後在「傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件」工作中參考。 存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需詳細資訊，請參閱 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>以程式設計方式設定傳送 SQL Server 物件工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
## <a name="transfer-sql-server-objects-task-editor-general-page"></a>傳送 SQL Server 物件工作編輯器 (一般頁面)
  使用 **[傳送 SQL Server 物件工作編輯器]** 對話方塊的 **[一般]** 頁面，即可命名和描述傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件工作。  
  
> [!NOTE]  
>  建立傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件工作的使用者，在來源伺服器物件上必須擁有適當的權限，來選取其供複製之用，並擁有權限來存取傳送之物件所在的目的地伺服器資料庫。  
  
### <a name="options"></a>選項。  
 **名稱**  
 輸入傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件工作的唯一名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件工作的描述。  
  
## <a name="transfer-sql-server-objects-task-editor-objects-page"></a>傳送 SQL Server 物件工作編輯器 (物件頁面)
  使用 [傳送 SQL Server 物件工作編輯器] 對話方塊的 [物件] 頁面，即可指定用於從某個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體將一或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件複製到另一個執行個體的屬性。 資料表、檢視、預存程序和使用者自訂函數是您可以複製的一些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件範例。  
  
> [!NOTE]  
>  建立傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件工作的使用者必須具有來源伺服器物件的足夠權限，才能選取它們以進行複製，也要具有存取會從該處傳送物件之目的地伺服器資料庫的權限。  
  
### <a name="static-options"></a>靜態選項  
 **SourceConnection**  
 在清單中選取一個 SMO 連線管理員，或按一下 **\<New connection...>** ，以建立新的來源伺服器連線。  
  
 **SourceDatabase**  
 在來源伺服器上選取會從中複製物件的資料庫。  
  
 **DestinationConnection**  
 在清單中選取一個 SMO 連線管理員，或按一下 **\<New connection...>** ，以建立新的目的地伺服器連線。  
  
 **DestinationDatabase**  
 在目的地伺服器上選取物件會被複製到的資料庫。  
  
 **DropObjectsFirst**  
 選取在複製之前，是否先在目的地伺服器上卸除選取的物件。  
  
 **IncludeExtendedProperties**  
 選取當物件從來源伺服器複製到目的地伺服器時是否包含擴充屬性。  
  
 **CopyData**  
 選取當物件從來源伺服器複製到目的地伺服器時是否包含資料。  
  
 **ExistingData**  
 指定如何將資料複製到目的地伺服器。 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**Replace**|目的地伺服器上的資料會被覆寫。|  
|**Append**|從來源伺服器複製的資料會附加至目的地伺服器上的現有資料。|  
  
> [!NOTE]  
>  只有 [CopyData] 設定為 [True] 時，才能使用 [ExistingData] 選項。  
  
 **CopySchema**  
 選取在傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件工作期間是否複製結構描述。  
  
> [!NOTE]  
>  **CopySchema** 只適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 **UseCollation**  
 選取物件的傳送是否應該包含在來源伺服器上所指定的定序。  
  
 **IncludeDependentObjects**  
 選取複製所選取物件時是否要串聯，以包含相依於選取要複製之物件的其他物件。  
  
 **CopyAllObjects**  
 選取工作會複製指定之來源資料庫中的所有物件，或僅複製選取的物件。  將此選項設定為 False，可讓您選擇在 [CopyAllObjects]  區段中選取要傳送的物件以及顯示動態選項。  
  
 **ObjectsToCopy**  
 展開 [ObjectsToCopy]  ，即可指定應從來源資料庫複製到目的地資料庫的物件。  
  
> [!NOTE]  
>  只有 **CopyAllObjects** 設定為 **False** 時，才能使用 **ObjectsToCopy**。  
  
 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]才支援用來複製下列類型之物件的選項：  
  
 組件  
  
 資料分割函數  
  
 資料分割配置  
  
 結構描述  
  
 使用者自訂彙總  
  
 使用者定義型別  
  
 XML 結構描述集合  
  
 **CopyDatabaseUsers**  
 指定資料庫使用者是否應該包含在傳送中。  
  
 **CopyDatabaseRoles**  
 指定資料庫角色是否應該包含在傳送中。  
  
 **CopySqlServerLogins**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入是否應該包含在傳送中。  
  
 **CopyObjectLevelPermissions**  
 指定物件層級權限是否應該包含在傳送中。  
  
 **CopyIndexes**  
 指定索引是否應該包含在傳送中。  
  
 **CopyTriggers**  
 指定觸發程序是否應該包含在傳送中。  
  
 **CopyFullTextIndexes**  
 指定全文檢索索引是否應該包含在傳送中。  
  
 **CopyPrimaryKeys**  
 指定主索引鍵是否應包含在傳送中。  
  
 **CopyForeignKeys**  
 指定外部索引鍵是否應該包含在傳送中。  
  
 **GenerateScriptsInUnicode**  
 指定產生的傳送指令碼是否為 Unicode 格式。  
  
### <a name="dynamic-options"></a>動態選項  
  
#### <a name="copyallobjects--false"></a>CopyAllObjects = False  
 **CopyAllTables**  
 選取工作會複製指定之來源資料庫中的所有資料表，或僅複製選取的資料表。  
  
 **TablesList**  
 按一下即可開啟 [選取資料表]  對話方塊。  
  
 **CopyAllViews**  
 選取工作會複製指定之來源資料庫中的所有檢視，或僅複製選取的檢視。  
  
 **ViewsList**  
 按一下即可開啟 [選取檢視]  對話方塊。  
  
 **CopyAllStoredProcedures**  
 選取工作會複製指定之來源資料庫中的所有使用者自訂預存程序，或僅複製選取的程序。  
  
 **StoredProceduresList**  
 按一下即可開啟 [選取預存程序]  對話方塊。  
  
 **CopyAllUserDefinedFunctions**  
 選取工作會複製指定之來源資料庫中的所有使用者自訂函數，或僅複製選取的 UDF。  
  
 **UserDefinedFunctionsList**  
 按一下即可開啟 [選取使用者自訂函數]  對話方塊。  
  
 **CopyAllDefaults**  
 選取工作會複製指定之來源資料庫中的所有預設值，或僅複製選取的預設值。  
  
 **DefaultsList**  
 按一下即可開啟 [選取預設值]  對話方塊。  
  
 **CopyAllUserDefinedDataTypes**  
 選取工作會複製指定之來源資料庫中的所有使用者自訂資料類型，或僅複製選取的使用者自訂資料類型。  
  
 **UserDefinedDataTypesList**  
 按一下即可開啟 [選取使用者自訂資料類型]  對話方塊。  
  
 **CopyAllPartitionFunctions**  
 選取工作會複製指定之來源資料庫中的所有使用者自訂資料分割函數，或僅複製選取的資料分割函數。 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]才支援。  
  
 **PartitionFunctionsList**  
 按一下即可開啟 [選取資料分割函數]  對話方塊。  
  
 **CopyAllPartitionSchemes**  
 選取工作會複製指定之來源資料庫中的所有資料分割配置，或僅複製選取的資料分割配置。 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]才支援。  
  
 **PartitionSchemesList**  
 按一下即可開啟 [選取資料分割配置]  對話方塊。  
  
 **CopyAllSchemas**  
 選取工作會複製指定之來源資料庫中的所有結構描述，或僅複製選取的結構描述。 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]才支援。  
  
 **SchemasList**  
 按一下即可開啟 [選取結構描述]  對話方塊。  
  
 **CopyAllSqlAssemblies**  
 選取工作會複製指定之來源資料庫中的所有 SQL 組件，或僅複製選取的 SQL 組件。 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]才支援。  
  
 **SqlAssembliesList**  
 按一下即可開啟 [選取 SQL 組件]  對話方塊。  
  
 **CopyAllUserDefinedAggregates**  
 選取工作會複製指定之來源資料庫中的所有使用者自訂彙總，或僅複製選取的使用者自訂彙總。 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]才支援。  
  
 **UserDefinedAggregatesList**  
 按一下即可開啟 [選取使用者自訂彙總]  對話方塊。  
  
 **CopyAllUserDefinedTypes**  
 選取工作會複製指定之來源資料庫中的所有使用者定義型別，或僅複製選取的 UDT。 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]才支援。  
  
 **UserDefinedTypes**  
 按一下即可開啟 [選取使用者定義型別]  對話方塊。  
  
 **CopyAllXmlSchemaCollections**  
 選取工作會複製指定之來源資料庫中的所有 XML 結構描述集合，或僅複製選取的 XML 結構描述集合。 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]才支援。  
  
 **XmlSchemaCollectionsList**  
 按一下即可開啟 [選取 XML 結構描述集合]  對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [傳送 SQL Server 物件工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/transfer-sql-server-objects-task-editor-general-page.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)   
 [大量匯入或大量匯出的資料格式 &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
