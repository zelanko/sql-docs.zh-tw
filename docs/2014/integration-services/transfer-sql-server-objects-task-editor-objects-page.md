---
title: 傳送 SQL Server 物件工作編輯器 （物件頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects Task Editor
ms.assetid: 8cc09118-70ac-4013-8308-d87f8411ca0c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3ae231e933e30613d45fe00eaa99d6a2d5c9c772
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054870"
---
# <a name="transfer-sql-server-objects-task-editor-objects-page"></a>傳送 SQL Server 物件工作編輯器 (物件頁面)
  使用 [傳送 SQL Server 物件工作編輯器]  對話方塊的 [物件]  頁面，即可指定用於從某個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體將一或多個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件複製到另一個執行個體的屬性。 資料表、檢視、預存程序和使用者自訂函數是您可以複製的一些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件範例。 如需有關這項工作的詳細資訊，請參閱＜ [Transfer SQL Server Objects Task](control-flow/transfer-sql-server-objects-task.md)＞。  
  
> [!NOTE]  
>  建立傳送 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件工作的使用者必須具有來源伺服器物件的足夠權限，才能選取它們以進行複製，也要具有存取會從該處傳送物件之目的地伺服器資料庫的權限。  
  
## <a name="static-options"></a>靜態選項  
 **SourceConnection**  
 在清單中選取 SMO 連線管理員，或按一下 [\<新增連線...>]  建立來源伺服器的新連線。  
  
 **SourceDatabase**  
 在來源伺服器上選取會從中複製物件的資料庫。  
  
 **DestinationConnection**  
 在清單中選取一個 SMO 連線管理員，或按一下 [\<新增連線...>]  ，以建立目的地伺服器的新連線。  
  
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
|**取代**|目的地伺服器上的資料會被覆寫。|  
|**附加**|從來源伺服器複製的資料會附加至目的地伺服器上的現有資料。|  
  
> [!NOTE]  
>  只有 [CopyData]  設定為 [True]  時，才能使用 [ExistingData]  選項。  
  
 **CopySchema**  
 選取在傳送 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件工作期間是否複製結構描述。  
  
> [!NOTE]  
>  **CopySchema** 只適用於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
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
  
 只有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]才支援用來複製下列類型之物件的選項：  
  
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
 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登入是否應該包含在傳送中。  
  
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
  
## <a name="dynamic-options"></a>動態選項  
  
### <a name="copyallobjects--false"></a>CopyAllObjects = False  
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
 選取工作會複製指定之來源資料庫中的所有使用者自訂資料分割函數，或僅複製選取的資料分割函數。 只有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]才支援。  
  
 **PartitionFunctionsList**  
 按一下即可開啟 [選取資料分割函數]  對話方塊。  
  
 **CopyAllPartitionSchemes**  
 選取工作會複製指定之來源資料庫中的所有資料分割配置，或僅複製選取的資料分割配置。 只有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]才支援。  
  
 **PartitionSchemesList**  
 按一下即可開啟 [選取資料分割配置]  對話方塊。  
  
 **CopyAllSchemas**  
 選取工作會複製指定之來源資料庫中的所有結構描述，或僅複製選取的結構描述。 只有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]才支援。  
  
 **SchemasList**  
 按一下即可開啟 [選取結構描述]  對話方塊。  
  
 **CopyAllSqlAssemblies**  
 選取工作會複製指定之來源資料庫中的所有 SQL 組件，或僅複製選取的 SQL 組件。 只有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]才支援。  
  
 **SqlAssembliesList**  
 按一下即可開啟 [選取 SQL 組件]  對話方塊。  
  
 **CopyAllUserDefinedAggregates**  
 選取工作會複製指定之來源資料庫中的所有使用者自訂彙總，或僅複製選取的使用者自訂彙總。 只有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]才支援。  
  
 **UserDefinedAggregatesList**  
 按一下即可開啟 [選取使用者自訂彙總]  對話方塊。  
  
 **CopyAllUserDefinedTypes**  
 選取工作會複製指定之來源資料庫中的所有使用者定義型別，或僅複製選取的 UDT。 只有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]才支援。  
  
 **UserDefinedTypes**  
 按一下即可開啟 [選取使用者定義型別]  對話方塊。  
  
 **CopyAllXmlSchemaCollections**  
 選取工作會複製指定之來源資料庫中的所有 XML 結構描述集合，或僅複製選取的 XML 結構描述集合。 只有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]才支援。  
  
 **XmlSchemaCollectionsList**  
 按一下即可開啟 [選取 XML 結構描述集合]  對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 工作](control-flow/integration-services-tasks.md)   
 [傳送 SQL Server 物件工作編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [大量匯入或大量匯出的資料格式 &#40;SQL Server&#41;](../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [SQL Server 安裝的安全性考量](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
