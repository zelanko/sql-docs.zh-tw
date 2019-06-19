---
title: 檢視 (Integration Services 目錄) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- views [Integration Services]
ms.assetid: d0294d43-4852-46dc-9afa-d0c19ea9aa03
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7133e0fc0b070c15be8f47df0ce4da650e2f12c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65802354"
---
# <a name="views-integration-services-catalog"></a>檢視 (Integration Services 目錄)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本節描述可用來管理 [!INCLUDE[tsql](../../includes/tsql-md.md)] 專案 (已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的執行個體) 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 檢視。  
  
 查詢 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 檢視，即可檢查物件、設定以及儲存在 **SSISDB** 目錄中的作業資料。  
  
 目錄的預設名稱為 SSISDB。 儲存在目錄中的物件包含了專案、封裝、參數、環境和作業歷程記錄。  
  
 您可以直接使用資料庫檢視和預存程序，或撰寫可呼叫 Managed API 的自訂程式碼。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 和 Managed API 會查詢檢視並呼叫本節中說明的預存程序，以執行許多工作。  
  
## <a name="in-this-section"></a>本節內容  
 [catalog.catalog_properties &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
 顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄的屬性。  
  
 [catalog.effective_object_permissions &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有物件顯示目前主體的有效權限。  
  
 [catalog.environment_variables &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有環境顯示環境變數詳細資料。  
  
 [catalog.environments &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有環境顯示環境詳細資料。 環境包含可由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案參考的變數。  
  
 [catalog.execution_parameter_values &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
 顯示執行執行個體期間由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝所使用的實際參數值。  
  
 [catalog.executions &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
 顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中封裝的執行執行個體。 以 [封裝執行工作] 執行的封裝會使用與父封裝的相同執行執行個體來執行。  
  
 [catalog.explicit_object_permissions &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md)  
 只顯示已明確指派給使用者的權限。  
  
 [catalog.extended_operation_info &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有作業顯示擴充資訊。  
  
 [catalog.folders &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-folders-ssisdb-database.md)  
 顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的資料夾。  
  
 [catalog.object_parameters &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中出現的所有封裝和專案顯示參數。  
  
 [catalog.object_versions &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
 顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的物件版本。 在這個版本中，這個檢視僅支援部分專案版本。  
  
 [catalog.operation_messages &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
 顯示在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中之作業期間所記錄的訊息。  
  
 [catalog.operations &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
 顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有作業的詳細資料。  
  
 [catalog.packages &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中出現的所有封裝顯示詳細資料。  
  
 [catalog.environment_references &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有專案顯示環境參考。  
  
 [catalog.projects &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中出現的所有專案顯示詳細資料。  
  
 [catalog.validations &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有專案和封裝驗證顯示詳細資料。  
  
[catalog.master_properties &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)  
顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master 的屬性。

[catalog.worker_agents &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)  
顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker 的資訊。  
