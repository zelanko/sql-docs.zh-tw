---
title: Integration Services 容器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS containers
- containers [Integration Services]
- containers [Integration Services], about containers
- control flow [Integration Services], containers
- SQL Server Integration Services containers
ms.assetid: 1b725922-ec59-4a47-9d55-e079463058f3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 87d8f17c8aa5b2e80939be7da8cbf81592bdd279
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915435"
---
# <a name="integration-services-containers"></a>整合服務容器

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  容器是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的物件，可提供結構給套件，並提供服務給工作。 它們支援封裝中的重複控制流程，且會將工作和容器分組成有意義的工作單位。 除了工作外，容器還可包含其他容器。  
  
 封裝會將容器用於下列用途：  
  
-   針對集合中的每個元素重複工作，例如資料夾中的檔案、結構描述或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件 (SMO) 的物件。 例如，封裝可執行位於多個檔案中的 Transact-SQL 陳述式。  
  
-   重複工作直到指定運算式評估結果為 **false**為止。 例如，封裝可傳送不同的電子郵件訊息七次，一週中的每一天各一次。  
  
-   將必須當做一個單位同時成功或失敗的工作和容器予以分組。 例如，封裝可將刪除或加入資料庫資料表中資料列的工作予以分組，然後在一個工作失敗時認可或回復所有工作。  
  
## <a name="container-types"></a>容器類型  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供四種用於建立封裝的容器類型。 下表列出這些容器類型。  
  
|容器|描述|  
|---------------|-----------------|  
|[Foreach 迴圈容器](../../integration-services/control-flow/foreach-loop-container.md)|使用列舉值重複執行控制流程。|  
|[For 迴圈容器](../../integration-services/control-flow/for-loop-container.md)|藉由測試條件重複執行控制流程。|  
|[時序容器](../../integration-services/control-flow/sequence-container.md)|將工作和容器分組成控制流程，這些控制流程是封裝控制流程的子集。|  
|[工作主機容器](../../integration-services/control-flow/task-host-container.md)|提供服務給單一工作。|  
  
 封裝和事件處理常式也是容器的類型。 如需相關資訊，請參閱 [Integration Services &#40;SSIS&#41; 封裝](../../integration-services/integration-services-ssis-packages.md)和 [Integration Services &#40;SSIS&#41; 事件處理常式](../../integration-services/integration-services-ssis-event-handlers.md)。  
  
### <a name="summary-of-container-properties"></a>容器屬性摘要  
 所有容器類型都有通用的屬性集。 如果您使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的圖形工具建立封裝，[屬性] 視窗會列出下列「Foreach 迴圈」、「For 迴圈」以及「時序」容器的屬性。 工作主機容器屬性會做為設定該工作主機封裝之工作的一部分來設定。 在您設定工作時，可同時設定「工作主機」屬性。  
  
|屬性|描述|  
|--------------|-----------------|  
|**DelayValidation**|布林值，指出是否延遲至執行階段才驗證容器。 這個屬性的預設值為 **False**。<br /><br /> 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.DelayValidation%2A>。|  
|**說明**|容器描述。 該屬性包含字串，但可能空白。<br /><br /> 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Description%2A>。|  
|**Disable**|布林值，指出容器是否執行。 這個屬性的預設值為 **False**。<br /><br /> 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Disable%2A>。|  
|**DisableEventHandlers**|布林值，指出與該容器關聯的事件處理常式是否執行。 這個屬性的預設值為 **False**。|  
|**FailPackageOnFailure**|布林值，指定如果容器中發生錯誤，封裝是否失敗。 這個屬性的預設值為 **False**。<br /><br /> 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailPackageOnFailure%2A>。|  
|**FailParentOnFailure**|布林值，指定如果容器中發生錯誤，父容器是否失敗。 這個屬性的預設值為 **False**。<br /><br /> 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailParentOnFailure%2A>。|  
|**ForcedExecutionValue**|如果 **ForceExecutionValue** 設定為 **True**，則是包含容器之選擇性執行值的物件。 這個屬性的預設值為 **0**。<br /><br /> 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForcedExecutionValue%2A>。|  
|**ForcedExecutionValueType**|**ForcedExecutionValue**的資料類型。 此屬性的預設值為 **Int32**。|  
|**ForceExecutionResult**|指定執行封裝或容器之強制結果的值。 可能的值為 **None**、 **Success**、 **Failure**和 **Completion**。 這個屬性的預設值為 **None**。<br /><br /> 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionResult%2A>。|  
|**ForceExecutionValue**|布林值，指定是否應該強制執行容器的選擇性執行值以包含特定值。 此屬性的預設值為 **False**。<br /><br /> 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionValue%2A>。|  
|**識別碼**|在建立封裝時所指派的容器 GUID。 這個屬性是唯讀的。<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ID%2A>第 1 課：建立 Windows Azure 儲存體物件<xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ID%2A>。|  
|**IsolationLevel**|容器交易的隔離等級。 可能的值為 **Unspecified**、 **Chaos**、 **ReadUncommitted**、 **ReadCommitted**、 **RepeatableRead**、 **Serializable**和 **Snapshot**。 此屬性的預設值為 **Serializable**。 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>。|  
|**LocaleID**|Microsoft Win32 地區設定。 此屬性的預設值為本機電腦作業系統的地區設定。<br /><br /> 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LocaleID%2A>。|  
|**LoggingMode**|指定容器記錄行為的值。 這些值為 **Disabled**、 **Enabled**和 **UseParentSetting**。 此屬性的預設值為 **UseParentSetting**。 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>。|  
|**MaximumErrorCount**|在容器停止執行之前，可發生的最大錯誤次數。 這個屬性的預設值為 **1**。<br /><br /> 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.MaximumErrorCount%2A>。|  
|**名稱**|容器的名稱。<br /><br /> 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Name%2A>。|  
|**TransactionOption**|容器的交易式參與。 可能的值為 **NotSupported**、 **Supported**、 **Required**。 此屬性的預設值為 **Supported**。 如需詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>。|  
  
 若要了解有關在以程式設計方式設定「Foreach 迴圈」、「For 迴圈」、「時序」及「工作主機」容器時，這些項目可用的所有屬性，請參閱下列 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] API 主題：  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForEachLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.Sequence  
  
-   T:Microsoft.SqlServer.Dts.Runtime.TaskHost  
  
## <a name="objects-that-extend-container-functionality"></a>延伸容器功能的物件  
 容器包括由可執行檔和優先順序條件約束所組成的控制流程，並可使用事件處理常式和變數。 工作主機容器則是例外：由於工作主機容器會封裝單一工作，因此不會使用優先順序條件約束。  
  
### <a name="executables"></a>可執行檔  
 可執行檔指的是容器層級工作，以及容器內的任何容器。 可執行檔可以是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所提供的其中一個工作和容器，也可以是自訂工作。 如需詳細資訊，請參閱 [Integration Services Tasks](../../integration-services/control-flow/integration-services-tasks.md)。  
  
### <a name="precedence-constraints"></a>優先順序條件約束  
 優先順序條件約束可將相同父容器中的工作，連結成已排序的控制流程。 如需詳細資訊，請參閱 [優先順序條件約束](../../integration-services/control-flow/precedence-constraints.md)。  
  
### <a name="event-handlers"></a>事件處理常式  
 容器層級的事件處理常式，可回應由容器或其中所含物件所引發的事件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 事件處理常式](../../integration-services/integration-services-ssis-event-handlers.md)。  
  
### <a name="variables"></a>變數  
 容器中所用的變數包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的容器層級系統變數，以及容器使用的使用者定義變數。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)。  
  
## <a name="break-points"></a>中斷點  
 當您在容器上設定中斷點，且中斷條件為 **[當容器接收 OnVariableValueChanged 事件時中斷]** 時，請在容器範圍中定義變數。  
  
## <a name="see-also"></a>另請參閱  
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
