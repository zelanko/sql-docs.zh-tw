---
title: SoapException 錯誤資料表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- SoapException class
ms.assetid: 3dbf1b5a-bd2a-4385-925d-5d095d72014c
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b2bd827eb6c1ff4abf5e531d54bbdde66b44249c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027239"
---
# <a name="soapexception-errors-table"></a>SoapException 錯誤資料表
  報表伺服器會根據在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中發生的錯誤，在 SOAP 例外狀況中產生錯誤與錯誤訊息。 下表顯示透過報表伺服器 Web 服務中的 **SoapException**，可從方法存取的錯誤。 這張表格是依照擲回例外狀況的方法加以組織。  
  
|方法|錯誤碼|  
|-----------------|----------------|  
|**ALL**|**rsEvaluationCopyExpired**|  
|**ALL**|**rsFailedToDecryptConfigInformation**|  
|**ALL**|**rsInvalidRSEditionConfiguration**|  
|**ALL**|**rsReportServerNotActivated**|  
|**ALL**|**rsServerBusy**|  
|**ALL**|**rsReportServerServiceUnavailable**|  
|**ALL**|**rsReportServerDisabled**|  
|**ALL**，但 **GetPermissions**、**GetRenderResource**、**GetSystemPermissions**、**ListEvents** 和 **ListSecureMethods** 除外|**rsAccessDenied**|  
|**ALL**，但 **CreateBatch**、**ExecuteBatch**、**GetSystemPolicies**、**GetSystemPermissions**、**GetSystemProperties**、**ListEvents**、**ListJobs**、**ListRoles**、**ListSchedules**、**ListSecureMethods**、**ListSubscriptions**、**ListSystemRoles**、**ListSystemTasks**、**ListTasks** 除外|**rsMissingParameter**|  
|**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateReportHistorySnapshot**、**CreateResource**、**CreateSubscription**、**DeleteItem**、**DeleteReportHistorySnapshot**、**DisableDataSource**、**EnableDataSource**、**FindItems**、**FlushCache**、**GetCacheOptions**、**GetDataSourceContents**、**GetExecutionOptions**、**GetPermissions**、**GetPolicies**、**GetProperties**、**GetReportDataSourcePrompts**、**GetReportDataSources**、**GetReportDefinition**、**GetReportHistoryLimit**、**GetReportHistoryOptions**、**GetReportLink**、**GetReportParameters**、**GetResourceContents**、**GetRoleProperties**、**GetServerDateTime**、**IheritParentSecurity**、**ListChildren**、**ListLinkedReports**、**ListReportHistory**、**ListReportsUsingDataSource**、**ListSchedules**、**ListSubscriptions**、**ListSubscriptionsUsingDataSource**、**MoveItem**、**Render**、**RenderStream**、**SetCacheOptions**、**SetDataSourceContents**、**SetExecutionOptions**、**SetPolicies**、**SetProperties**、**SetReportDataSources**、**SetReportDefinition**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetReportLink**、**SetReportParameters**、**SetResourceContents**、**UpdateReportExecutionSnapshot**、**ValidateExtensionSettings**|**rsItemNotFound**|  
|**CancelBatch**、**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateReportHistorySnapshot**、**CreateResource**、**CreateRole**、**CreateSchedule**、**CreateSubscription**、**DeleteItem**、**DeleteReportHistorySnapshot**、**DeleteRole**、**DeleteSchedule**、**DeleteSubscription**、**DisableDataSource**、**EnableDataSource**、**ExecuteBatch**、**FindItems**、**FlushCache**、**GetResourceContents**、**GetServerDateTime**、**MoveItem**、**PauseSchedule**、**ResumeSchedule**、**SetCacheOptions**、**SetDataDrivenSubscriptionProperties**、**SetDataSourceContents**、**SetExecutionOptions**、**SetPolicies**、**SetProperties**、**SetReportDataSources**、**SetReportDefinition**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetReportLink**、**SetReportParameters**、**SetResourceContents**、**SetRoleProperties**、**SetScheduleProperties**、**SetSubscriptionProperties**、**SetSystemPolicies**、**SetSystemProperties**、**UpdateReportExecutionSnapshot**、**ValidateExtensionSettings**|**rsBatchNotFound**|  
|**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateReportHistorySnapshot**、**CreateResource**、**CreateSubscription**、**DeleteItem**、**DeleteReportHistorySnapshot**、**DisableDataSource**、**EnableDataSource**、**FindItems**、**FlushCache**、**GetCacheOptions**、**GetDataSourceContents**、**GetExecutionOptions**、**GetItemType**、**GetPermissions**、**GetPolicies**、**GetProperties**、**GetReportDataSourcePrompts**、**GetReportDataSources**、**GetReportDefinition**、**GetReportHistoryLimit**、**GetReportHistoryOptions**、**GetReportLink**、**GetResourceContents**、**GetServerDateTime**、**IheritParentSecurity**、**ListChildren**、**ListLinkedReports**、**ListReportHistory**、**ListSchedules**、**ListSubscriptionsUsingDataSource**、**MoveItem**、**Render**、**RenderStream**、**SetCacheOptions**、**SetDataSourceContents**、**SetExecutionOptions**、**SetPolicies**、**SetProperties**、**SetReportDataSources**、**SetReportDefinition**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetReportLink**、**SetReportParameters**、**SetResourceContents**、**SetSubscriptionProperties**、**UpdateReportExecutionSnapshot**、**ValidateExtensionSettings**|**rsInvalidItemPath**|  
|**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateReportHistorySnapshot**、**CreateResource**、**CreateSubscription**、**DeleteReportHistorySnapshot**、**DisableDataSource**、**EnableDataSource**、**FindItems**、**FlushCache**、**GetCacheOptions**、**GetDataSourceContents**、**GetExecutionOptions**、**GetReportDataSourcePrompts**、**GetReportDataSources**、**GetReportDefinition**、**GetReportHistoryLimit**、**GetReportHistoryOptions**、**GetReportLink**、**GetReportParameters**、**GetResourceContents**、**GetServerDateTime**、**GetSystemProperties**、**ListChildren**、**ListLinkedReports**、**ListReportHistory**、**ListReportsUsingDataSource**、**ListSchedules**、**ListSubscriptions**、**ListSubscriptionsUsingDataSource**、**MoveItem**、**Render**、**RenderStream**、**SetCacheOptions**、**SetDataSourceContents**、**SetExecutionOptions**、**SetReportDataSources**、**SetReportDefinition**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetReportLink**、**SetReportParameters**、**SetResourceContents**、**UpdateReportExecutionSnapshot**、**ValidateExtensionSettings**|**rsWrongItemType**|  
|**CreateReport**、**CreateResource**、**DeleteReportHistorySnapshot**、**DeleteSchedule**、**DeleteSubscription**、**GetDataDrivenSubscriptionProperties**、**GetSubscriptionProperties**、**ListChildren**、**ListScheduledReports**、**PauseSchedule**、**Render**、**RenderStream**、**ResumeSchedule**、**SetCacheOptions**、**SetDataDrivenSubscriptionProperties**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetScheduleProperties**、**SetSubscriptionProperties**|**rsParameterTypeMismatch**|  
|**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateSchedule**、**CreateSubscription**、**FindItems**、**GetReportParameters**、**PrepareQuery**、**Render**、**SetCacheOptions**、**SetDataDrivenSubscriptionProperties**、**SetDataSourceContents**、**SetPolicies**、**SetReportDataSources**、**SetReportParameters**、**SetScheduleProperties**、**SetSubscriptionProperties**、**SetSystemPolicies**|**rsMissingElement**|  
|**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateSchedule**、**CreateSubscription**、**PrepareQuery**、**Render**、**SetCacheOptions**、**SetDataDrivenSubscriptionProperties**、**SetDataSourceContents**、**SetProperties**、**SetReportDataSources**、**SetReportParameters**、**SetScheduleProperties**、**SetSubscriptionProperties**、**SetSystemProperties**|**rsInvalidElement**|  
|**CreateDataDrivenSubscription**、**CreateSchedule**、**CreateSubscription**、**FindItems**、**GetRenderResource**、**PrepareQuery**、**Render**、**RenderStream**、**SetCacheOptions**、**SetDataDrivenSubscriptionProperties**、**SetExecutionOptions**、**SetProperties**、**SetReportHistoryOptions**、**SetReportParameters**、**SetScheduleProperties**、**SetSubscriptionProperties**、**SetSystemProperties**|**rsElementTypeMismatch**|  
|**CreateDataSource**、**CreateRole**、**GetDataDrivenSubscriptionProperties**、**GetRenderResource**、**ListExtensions**、**Render**、**SetDataDrivenSubscriptionProperties**、**SetDataSourceContents**、**SetExecutionOptions**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetScheduleProperties**|**rsInvalidParameter**|  
|**CreateDataDrivenSubscription**、**CreateReportHistorySnapshot**、**CreateSubscription**、**PrepareQuery**、**SetDataDrivenSubscriptionProperties**、**SetExecutionOptions**、**SetReportHistoryOptions**、**SetSubscriptionProperties**|**rsInvalidDataSourceCredentialSetting**|  
|**CreateDataDrivenSubscriptionProperties**、**CreateReportHistorySnapshot**、**CreateSchedule**、**CreateSubscription**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**、**UpdateReportExecutionSnapshot**|**rsReportParameterValueNotSet**|  
|**CreateDataDrivenSubscription**、**CreateSubscription**、**GetExtensionSettings**、**GetRenderResource**、**Render**、**RenderStream**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsMultipleExtensionsFoundInAssembly**|  
|**CreateDataDrivenSubscriptionProperties**、**CreateSubscription**、**Render**、**SetCacheOptions**、**SetExecutionOptions**、**SetReportParameters**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsReportParameterTypeMismatch**|  
|**CreateSchedule**、**CreateSubscription**、**DeleteSchedule**、**PauseSchedule**、**ResumeSchedule**、**SetCacheOptions**、**SetExecutionOptions**、**SetScheduleProperties**、**SetSubscriptionProperties**|**rsSchedulerNotResponding**|  
|**DeleteSchedule**、**GetScheduleProperties**、**ListScheduledReports**、**PauseSchedule**、**ResumeSchedule**、**SetCacheOptions**、**SetExecutionOptions**、**SetScheduleProperties**|**rsScheduleNotFound**|  
|**CreateDataDrivenSubscriptionProperties**、**CreateSubscription**、**Render**、**SetReportParameters**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsReadOnlyReportParameter**|  
|**CreateDataDrivenSubscriptionProperties**、**CreateSubscription**、**GetReportParameters**、**Render**、**SetReportParameters**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsUnknownReportParameter**|  
|**DeleteSubscription**、**GetDataDrivenSubscriptionProperties**、**GetSubscriptionProperties**、**SetDataDrivenSubscriptionProperties**、**SetExecutionOptions**、**SetSubscriptionProperties**|**rsSubscriptionNotFound**|  
|**CreateDataDrivenSubscription**、**CreateSubscription**、**GetExtensionSettings**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsDeliveryExtensionNotFound**|  
|**CreateDataDrivenSubscription**、**CreateSubscription**、**GetExtensionSettings**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsDeliveryError**|  
|**CreateDataDrivenSubscription**、**GetDataDrivenSubscriptionProperties**、**PrepareQuery**、**SetDataDrivenSubscriptionProperties**|**rsSecureConnectionRequired**|  
|**CreateDataDrivenSubscription**、**CreateSubscription**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsCannotSubscribeToEvent**|  
|**CreateDataDrivenSubscription**、**CreateSubscription**、**FireEvent**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsUnknownEventType**|  
|**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateResource**、**MoveItem**|**rsItemPathLengthExceeded**|  
|**CopyItem**、**CreateFolder**、**CreateReport**、**CreateResource**、**DeleteItem**|**rsReservedItem**|  
|**CreateDataSource**、**SetDataSourceContents**、**SetReportDataSources**|**rsInvalidElementCombination**|  
|**SetCacheOptions**、**SetExecutionOptions**、**SetReportHistoryOptions**|**rsInvalidParameterCombination**|  
|**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateResource**、**MoveItem**|**rsInvalidItemName**|  
|**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateResource**、**MoveItem**|**rsItemAlreadyExists**|  
|**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateResource**、**SetProperties**|**rsReadOnlyProperty**|  
|**GetPolicies**、**GetSystemPolicies**、**SetPolicies**、**SetSystemPolicies**|**rsInvalidPolicyDefinition**|  
|**SetCacheOptions**、**SetDataSourceContents**、**SetReportDataSources**、**SetReportParameters**|**rsOperationPreventsUnattendedExecution**|  
|**CreateReportHistorySnapshot**、**Render**、**PrepareQuery**、**UpdateReportExecutionSnapshot**|**rsInvalidDataSourceReference**|  
|**CreateReportHistorySnapshot**、**PrepareQuery**、**Render**、**UpdateReportExecutionSnapshot**|**rsDataSourceDisabled**|  
|**CreateReport**、**PrepareQuery**、**SetReportDefinition**|**rsProcessingError**|  
|**GetRenderResource**、**Render**、**RenderStream**|**rsInvalidReportLink**|  
|**DeleteReportHistorySnapshot**、**Render**、**RenderStream**|**rsReportHistoryNotFound**|  
|**SetCacheOptions**、**SetExecutionOptions**、**SetReportHistoryOptions**|**rsReportMayNotBeScheduled**|  
|**CreateDataDrivenSubscription**、**GetDataDrivenSubscriptionProperties**、**SetDataDrivenSubscriptionProperties**|**rsOperationNotSupported**|  
|**CreateDataSource**、**SetDataSourceContents**、**SetReportDataSources**|**rsDataExtensionNotFound**|  
|**DeleteRole**、**SetPolicies**、**SetRoleProperties**|**rsRoleNotFound**|  
|**DeleteReportHistorySnapshot**、**Render**、**RenderStream**|**rsParametersNotSpecified**|  
|**GetReportParameters**、**SetReportParameters**|**rsNotSupported**|  
|**SetReportParameters**、**UpdateReportExecutionSnapshot**|**rsReportSnapshotNotEnabled**|  
|**CreateSchedule**、**SetScheduleProperties**|**rsScheduleAlreadyExists**|  
|**CreateRole**、**SetRoleProperties**|**rsTaskNotFound**|  
|**CreateRole**、**SetRoleProperties**|**rsMixedTasks**|  
|**ListSubscriptions**、**SetPolicies**|**rsUnknownUserName**|  
|**MoveItem**|**rsInvalidMove**|  
|**RenderStream**|**rsStreamNotFound**|  
|**RenderStream**|**rsMissingSessionId**|  
|**轉譯**|**rsReportNotReady**|  
|**轉譯**|**rsAssemblyNotPermissioned**|  
|**SetExecutionOptions**|**rsReportSnapshotEnabled**|  
|**FindItems**|**rsInvalidSearchOperator**|  
|**SetReportDataSources**|**rsDataSourceNotFound**|  
|**PrepareQuery**、**Render**|**rsDataSourceNoPrompt**|  
|**PrepareQuery**|**rsCannotPrepareQuery**|  
|**DeleteRole**|**rsReservedRole**|  
|**CreateRole**|**rsEmptyRole**|  
|**InheritParentSecurity**|**rsInheritedPolicy**|  
|**CreateRole**|**rsRoleAlreadyExists**|  
|**InheritParentSecurity**|**rsCannotDeleteRootPolicy**|  
|**CancelJob**|**rsJobWasCanceled**|  
|**ListSecureMethods**|**rsServerConfigurationError**|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的例外狀況處理簡介](../introducing-exception-handling-in-reporting-services.md)   
 [錯誤和事件參考 &#40;Reporting Services&#41;](../../troubleshooting/errors-and-events-reference-reporting-services.md)   
 [Reporting Services SoapException 類別](reporting-services-soapexception-class.md)   
 [使用 Detail 屬性來處理特定的錯誤](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
