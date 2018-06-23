---
title: 系統變數 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- containers [Integration Services], variables
- tasks [Integration Services], variables
- system variables [Integration Services]
- event handlers [Integration Services], variables
- variables [Integration Services], system
ms.assetid: efecd0d4-1489-4eba-a8fe-275d647058b8
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b820a671418fc3126f2b5904f9a2a1c0c881eaa9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134217"
---
# <a name="system-variables"></a>系統變數
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供一組儲存執行封裝及其物件之資訊的系統變數。 這些變數可以用於運算式及屬性運算式，以自訂封裝、容器、工作及事件處理常式。  
  
 所有的變數 (系統變數和使用者自訂變數) 都可在「執行 SQL」工作用來將變數對應至參數的參數繫結中使用。  
  
## <a name="system-variables-for-packages"></a>封裝的系統變數  
 下表描述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 為封裝提供的系統變數。  
  
|系統變數|資料類型|描述|  
|---------------------|---------------|-----------------|  
|**CancelEvent**|Int32|[Windows 事件] 物件的控制代碼，可以讓工作發出信號以指出該工作應該停止執行。|  
|`ContainerStartTime`|DateTime|容器的開始時間。|  
|**CreationDate**|DateTime|建立封裝的日期。|  
|`CreatorComputerName`|String|建立封裝的電腦。|  
|**CreatorName**|String|建立封裝之人員的姓名。|  
|`ExecutionInstanceGUID`|String|執行封裝之執行個體的唯一識別碼。|  
|`FailedConfigurations`|String|失敗的封裝組態名稱。|  
|`IgnoreConfigurationsOnLoad`|布林|指出載入封裝時是否忽略封裝組態。|  
|**InteractiveMode**|布林|指示封裝是否以互動模式執行。 如果封裝在「[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」中執行，則此屬性設為 `True`。 如果封裝執行時使用**DTExec**命令提示字元公用程式的屬性設定為`False`。|  
|`LocaleId`|Int32|封裝使用的地區設定。|  
|**MachineName**|String|執行封裝之電腦的名稱。|  
|**OfflineMode**|布林|指出封裝是否處於離線模式。 離線模式不會取得與資料來源的連接。|  
|**PackageID**|String|封裝的唯一識別碼。|  
|**PackageName**|String|封裝名稱。|  
|**StartTime**|DateTime|封裝開始執行的時間。|  
|`ServerExecutionID`|Int64|在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器上執行之封裝的執行識別碼。<br /><br /> 預設值為零。 只有在 ISServerExec 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器上執行封裝時，才會變更此值。 有子封裝時，此值會從父封裝傳遞至子封裝。|  
|**UserName**|String|啟動封裝之使用者的帳戶。 使用者名稱必須以網域名稱來限定。|  
|**VersionBuild**|Int32|封裝版本。|  
|**VersionComment**|String|有關封裝版本的註解。|  
|**VersionGUID**|String|版本的唯一識別碼。|  
|**VersionMajor**|Int32|封裝的主要版本。|  
|**VersionMinor**|Int32|封裝的次要版本。|  
  
## <a name="system-variables-for-containers"></a>容器的系統變數  
 下表描述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 為 For 迴圈、Foreach 迴圈及時序容器提供的系統變數。  
  
|系統變數|資料類型|描述|容器|  
|---------------------|---------------|-----------------|---------------|  
|`LocaleId`|Int32|容器使用的地區設定。|For 迴圈容器<br /><br /> Foreach 迴圈容器<br /><br /> 時序容器|  
  
## <a name="system-variables-for-tasks"></a>工作的系統變數  
 下表描述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 為工作提供的系統變數。  
  
|系統變數|資料類型|描述|  
|---------------------|---------------|-----------------|  
|**CreationName**|String|工作的名稱。|  
|`LocaleId`|Int32|工作使用的地區設定。|  
|**TaskID**|String|工作執行個體的唯一識別碼。|  
|**TaskName**|String|工作執行個體的名稱。|  
|`TaskTransactionOption`|Int32|工作使用的交易選項。|  
  
## <a name="system-variables-for-event-handlers"></a>事件處理常式的系統變數  
 下表描述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 為事件處理常式提供的系統變數。 並非所有變數都可用於所有事件處理常式。  
  
|系統變數|資料類型|描述|事件處理常式|  
|---------------------|---------------|-----------------|-------------------|  
|**取消**|布林|指示當發生錯誤、警告或查詢取消時，事件處理常式是否停止執行。|OnError 事件處理常式<br /><br /> OnWarning 事件處理常式<br /><br /> OnQueryCancel 事件處理常式|  
|**ErrorCode**|Int32|錯誤識別碼。|OnError 事件處理常式<br /><br /> OnInformation 事件處理常式<br /><br /> OnWarning 事件處理常式|  
|**ErrorDescription**|String|錯誤的描述。|OnError 事件處理常式<br /><br /> OnInformation 事件處理常式<br /><br /> OnWarning 事件處理常式|  
|**ExecutionStatus**|布林|目前執行狀態。|OnExecStatusChanged 事件處理常式|  
|`ExecutionValue`|DBNull|執行值。|OnTaskFailed 事件處理常式|  
|`LocaleId`|Int32|事件處理常式使用的地區設定。|所有事件處理常式|  
|**PercentComplete**|Int32|已完成工作的百分比。|OnProgress 事件處理常式|  
|**ProgressCountHigh**|Int32|64 位元值的較高部份，指示 OnProgress 事件處理的作業總數。|OnProgress 事件處理常式|  
|`ProgressCountLow`|Int32|64 位元值的較低部份，指示 OnProgress 事件處理的作業總數。|OnProgress 事件處理常式|  
|**ProgressDescription**|String|進度的描述。|OnProgress 事件處理常式|  
|`Propagate`|布林|指示是否將事件傳播至較高層級的事件處理常式。<br /><br /> 注意： 的值`Propagate`變數驗證封裝期間，會忽略。<br /><br /> 如果您在子封裝中，將 `Propagate` 設定為 `False`，這就無法防止事件向上擴展到父封裝。|所有事件處理常式|  
|`SourceDescription`|String|事件處理常式中引發事件之可執行檔的描述。|所有事件處理常式|  
|`SourceID`|String|事件處理常式中引發事件之可執行檔的唯一識別碼。|所有事件處理常式|  
|**SourceName**|String|事件處理常式中引發事件之可執行檔的名稱。|所有事件處理常式|  
|`VariableDescription`|String|變數描述。|OnVariableValueChanged 事件處理常式|  
|`VariableID`|String|變數的唯一識別碼。|OnVariableValueChanged 事件處理常式|  
  
## <a name="system-variables-in-parameter-bindings"></a>參數繫結中的系統變數  
 執行封裝時，將系統變數的值儲存在資料表中通常很有幫助。 例如，動態建立資料表並在資料表資料行中寫入建立資料表之封裝執行個體 GUID 的封裝。  
  
 如果使用系統變數對應至「執行 SQL」工作使用之 SQL 陳述式中的參數，您就必須將每個參數繫結的資料類型設定為系統變數的資料類型。 否則，系統變數值的翻譯可能會出錯。 例如，如果在具有 GUID 資料類型的參數繫結中使用 `ExecutionInstanceGUID` 系統變數，而此系統變數具有字串資料類型並包含代表封裝執行個體之 GUID 的字串，封裝執行個體 GUID 的翻譯便會出錯。  
  
 此規則也適用於使用者自訂變數。 但是，由於系統變數的資料類型無法變更，而且您必須修改這些變數的用法以符合其資料類型，因此使用者自訂變數比較有彈性。 參數繫結中使用之使用者自訂變數所定義的資料類型，通常與其對應參數的資料類型相容。  
  
## <a name="related-tasks"></a>相關工作  
 [將查詢參數對應至變數，在執行 SQL 工作](control-flow/execute-sql-task.md)  
  
  