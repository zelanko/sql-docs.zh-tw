---
title: 設定套件屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- checkpoints [Integration Services]
- execution properties [Integration Services]
- packages [Integration Services], properties
- identification properties [Integration Services]
- passwords [Integration Services]
- SSIS packages, properties
- transaction properties [Integration Services]
- updating package properties
- forced execution value properties [Integration Services]
- security properties [Integration Services]
- version properties [Integration Services]
- SQL Server Integration Services packages, properties
ms.assetid: 13f81c3e-2b18-4f83-b445-a2f4a2c560aa
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 12e500402c68da2e38fd88c5d061644a7f51fd58
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104844"
---
# <a name="set-package-properties"></a>設定封裝屬性
  當您使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 所提供的圖形介面，在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中建立封裝時，可以在 [屬性] 視窗中設定封裝物件的屬性。  
  
 **[屬性]** 視窗提供分類且按字母排列的屬性清單。 若要依類別來排列 **[屬性]** 視窗，請按一下 [分類] 圖示。  
  
 依類別排列時， **[屬性]** 視窗會將屬性分組成下列類別：  
  
-   [檢查點](#Checkpoints)  
  
-   [執行](#Execution)  
  
-   [強制執行的值](#ForcedExecutionValue)  
  
-   [識別](#Identification)  
  
-   [其他](#Misc)  
  
-   [Security](#Security)  
  
-   [交易](#Transactions)  
  
-   [版本](#Version)  
  
 如需無法在 [屬性] 視窗中設定的其他套件屬性的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.Package>。  
  
### <a name="to-set-package-properties-in-the-properties-window"></a>在屬性視窗中設定封裝屬性  
  
-   [設定套件的屬性](../../2014/integration-services/set-the-properties-of-a-package.md)  
  
## <a name="properties-by-category"></a>依類別列出屬性  
 下表會依類別列出封裝屬性。  
  
###  <a name="Checkpoints"></a> 檢查點  
 您可以使用此類別中的屬性，從封裝控制流程中的失敗點重新啟動封裝，而不用從控制流程的開頭重新執行封裝。 如需詳細資訊，請參閱 [使用檢查點來重新啟動封裝](packages/restart-packages-by-using-checkpoints.md)。  
  
|屬性|描述|  
|--------------|-----------------|  
|`CheckpointFileName`|擷取可讓封裝重新啟動的檢查點資訊之檔案名稱。 當封裝成功完成時，便會刪除此檔案。|  
|`CheckpointUsage`|指定何時可以重新啟動封裝。 值是`Never`， `IfExists`，和`Always`。 這個屬性的預設值是`Never`，指出無法重新啟動封裝。 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DTSCheckpointUsage>。|  
|`SaveCheckpoints`|指定是否要在封裝執行時將檢查點寫入檢查點檔案。 這個屬性的預設值是`False`。|  
  
> [!NOTE]  
>  dtexec 的 `/CheckPointing on` 選項相當於將封裝的 `SaveCheckpoints` 屬性設為 True，以及將 `CheckpointUsage` 屬性設為 Always。 如需詳細資訊，請參閱 [dtexec Utility](packages/dtexec-utility.md)。  
  
###  <a name="Execution"></a> 執行  
 此類別中的屬性會設定封裝物件的執行階段行為。  
  
|屬性|描述|  
|--------------|-----------------|  
|`DelayValidation`|指出封裝驗證是否延遲到封裝執行時。 這個屬性的預設值是`False`。|  
|**Disable**|指出是否停用封裝。 這個屬性的預設值是`False`。|  
|`DisableEventHandlers`|指定封裝事件處理常式是否執行。 這個屬性的預設值是`False`。|  
|`FailPackageOnFailure`|指定如果封裝元件中發生錯誤則封裝是否會失敗。 唯一有效的值，這個屬性是`False`。|  
|`FailParentOnError`|指定如果子容器中發生錯誤則父容器是否會失敗。 此屬性的預設值為 `False`。|  
|`MaxConcurrentExecutables`|封裝可以同時執行的可執行檔數目。 此屬性的預設值為 **-1**，表示沒有限制。|  
|`MaximumErrorCount`|在封裝停止執行前可發生的最大錯誤數目。 這個屬性的預設值為 **1**。|  
|`PackagePriorityClass`|封裝執行緒的 Win32 執行緒優先權等級。 值是`Default`， `AboveNormal`， `Normal`， `BelowNormal`， `Idle`。 這個屬性的預設值是`Default`。 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DTSPriorityClass>。|  
  
###  <a name="ForcedExecutionValue"></a> 強制執行的值  
 此類別中的屬性會針對封裝設定選擇性的執行值。  
  
|屬性|描述|  
|--------------|-----------------|  
|`ForcedExecutionValue`|如果設定為 ForceExecutionValue `True`，指定封裝所傳回的選擇性執行值的值。 這個屬性的預設值為 **0**。|  
|`ForcedExecutionValueType`|ForcedExecutionValue 的資料類型。 這個屬性的預設值是`Int32`。|  
|`ForceExecutionValue`|布林值，指定是否應該強制執行容器的選擇性執行值以包含特定值。 這個屬性的預設值是`False`。|  
  
###  <a name="Identification"></a> 識別  
 此類別中的屬性會提供唯一識別碼與封裝名稱等資訊。  
  
|屬性|描述|  
|--------------|-----------------|  
|`CreationDate`|建立封裝的日期。|  
|`CreatorComputerName`|用來建立封裝的電腦名稱。|  
|`CreatorName`|封裝建立者名稱。|  
|`Description`|封裝功能描述。|  
|`ID`|在建立封裝時所指派的封裝 GUID。 此屬性是唯讀的。 若要產生新的隨機值，如`ID`屬性中，選取**\<產生新的識別碼 >** 下拉式清單中。|  
|`Name`|封裝名稱。|  
|`PackageType`|封裝類型。 值是`Default`， `DTSDesigner`， `DTSDesigner100`， `DTSWizard`， `SQLDBMaint`，和`SQLReplication`。 這個屬性的預設值是`Default`。 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>。|  
  
###  <a name="Misc"></a> 其他  
 此類別中的屬性是用來存取封裝所用的組態和運算式，以及提供有關封裝的地區設定與記錄模式等資訊。 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](expressions/use-property-expressions-in-packages.md)。  
  
|屬性|描述|  
|--------------|-----------------|  
|`Configurations`|封裝使用的組態集合。 請按一下瀏覽按鈕 **(…)** 以檢視和設定封裝組態。|  
|`Expressions`|請按一下瀏覽按鈕 **(…)** 以建立封裝屬性的運算式。<br /><br /> 注意： 您可以建立屬性運算式之所有封裝屬性的物件模型包含，不只是將在 [屬性] 視窗中列出的屬性。<br /><br /> 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](expressions/use-property-expressions-in-packages.md)。<br /><br /> 若要檢視現有的屬性運算式，請展開 `Expressions`。 按一下運算式文字方塊中的瀏覽按鈕 **(…)** ，以修改及評估運算式。|  
|`ForceExecutionResult`|封裝的執行結果。 值是`None`， `Success`， `Failure`，和`Completion`。 這個屬性的預設值是`None`。 如需詳細資訊，請參閱 T:Microsoft.SqlServer.Dts.Runtime.DTSForcedExecResult。|  
|`LocaleId`|Microsoft Win32 地區設定。 此屬性的預設值為本機電腦作業系統的地區設定。|  
|`LoggingMode`|指定封裝記錄行為的值。 值是`Disabled`， `Enabled`，和`UseParentSetting`。 這個屬性的預設值是`UseParentSetting`。 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>。|  
|`OfflineMode`|指出封裝是否處於離線模式。 此屬性是唯讀的。 這個屬性是在專案層級設定。 通常，「 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」會試圖連接到封裝所使用的每一個資料來源，以驗證與來源及目的地相關聯的中繼資料。 如果資料來源無法使用，您可以啟用 **[SSIS]** 功能表上的 **[離線工作]** (甚至在開啟封裝之前)，以防止發生這些連接而造成驗證錯誤的結果。 您也可以啟用 [離線工作]  來加速設計師中的作業，並只有在想要驗證封裝時才停用這個功能。|  
|`SuppressConfigurationWarnings`|指出是否會抑制組態所產生的警告。 這個屬性的預設值是`False`。|  
|`UpdateObjects`|表示如果有較新版本時，是否更新封裝以使用所包含物件的較新版本。 例如，如果這個屬性設定為`True`，包含 「 大量插入 」 工作的封裝會更新為使用新版 「 大量插入工作[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]提供。 這個屬性的預設值是`False`。|  
  
###  <a name="Security"></a> 安全性  
 此類別中的屬性是用來設定封裝的保護等級。 如需詳細資訊，請參閱 [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md)。  
  
|屬性|描述|  
|--------------|-----------------|  
|`PackagePassword`|封裝保護等級的密碼 (`EncryptSensitiveWithPassword`和`EncryptAllWithPassword`)，要求先提供密碼。|  
|`ProtectionLevel`|封裝保護等級。 值是`DontSaveSensitive`， `EncryptSensitiveWithUserKey`， `EncryptSensitiveWithPassword`， `EncryptAllWithPassword`，並**ServerStorage**。 這個屬性的預設值是`EncryptSensitiveWithUserKey`。 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel>。|  
  
###  <a name="Transactions"></a> 交易  
 此類別中的屬性會設定封裝的隔離等級和交易選項。 如需詳細資訊，請參閱 [Integration Services 交易](integration-services-transactions.md)。  
  
|屬性|描述|  
|--------------|-----------------|  
|`IsolationLevel`|封裝交易的隔離等級。  這個屬性的預設值是`Serializable`。 有效的值為 <br />`Unspecified`<br />`Chaos`<br />`ReadUncommitted`<br />`ReadCommitted`<br />`RepeatableRead`<br />`Serializable`<br />`Snapshot`.<br /><br /> 只有當 `IsolationLevel` 屬性的值設定為 `TransactionOption` 時，系統才會將 `Required` 屬性套用到封裝交易。<br /><br /> 值`IsolationLevel`當下列條件成立時，則會忽略子容器所要求的屬性：<br /><br /> 子容器的 `TransactionOption` 屬性值為 `Supported`。<br />子容器會聯結父容器的交易。<br /><br /> 只有當容器起始新的交易時，才會接受容器所要求的 `IsolationLevel` 屬性值。 當下列條件都成立時，容器會起始新的交易：<br /><br /> 容器的 `TransactionOption` 屬性值為 `Required`。<br />父容器尚未啟動交易。<br /><br /> <br /><br /> 注意︰`Snapshot`的值`IsolationLevel`屬性是與封裝交易不相容。 因此，您無法使用`IsolationLevel`屬性來設定封裝交易的隔離等級`Shapshot`。 相反地，將封裝交易設定為使用 SQL 查詢`Snapshot`。 如需詳細資訊，請參閱 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)。<br /><br /> 如需有關 `IsolationLevel` 屬性的詳細資訊，請參閱＜<xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>＞。|  
|`TransactionOption`|封裝的交易式參與。 可能的值為 `NotSupported`、`Supported`、`Required`。 這個屬性的預設值是`Supported`。 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>。|  
  
###  <a name="Version"></a> 版本  
 此類別中的屬性會提供有關封裝物件版本的資訊。  
  
|屬性|描述|  
|--------------|-----------------|  
|`VersionBuild`|封裝建置的版本號碼。|  
|`VersionComments`|封裝的版本註解。|  
|`VersionGUID`|封裝版本的 GUID。 此屬性是唯讀的。|  
|`VersionMajor`|封裝的最新主要版本。|  
|`VersionMinor`|封裝的最新次要版本。|  
  
  
