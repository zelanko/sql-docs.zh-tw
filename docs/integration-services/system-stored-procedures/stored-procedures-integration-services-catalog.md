---
title: 預存程序 (Integration Services 目錄) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- stored procedures [Integration Services]
ms.assetid: a6ccd884-108f-4fb6-95ad-00b9cb65d5d6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e1eea2f9e83069b18b47b1563e60a0c31c0bfcb0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296682"
---
# <a name="stored-procedures-integration-services-catalog"></a>預存程序 (Integration Services 目錄)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本節描述可用來管理 [!INCLUDE[tsql](../../includes/tsql-md.md)] 專案 (已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的執行個體) 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序。  
  
 呼叫 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 預存程序，即可新增、移除、修改或執行 **SSISDB** 目錄中所儲存的物件。  
  
 目錄的預設名稱為 SSISDB。 儲存在目錄中的物件包含了專案、封裝、參數、環境和作業歷程記錄。  
  
 您可以直接使用資料庫檢視和預存程序，或撰寫可呼叫 Managed API 的自訂程式碼。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 和 Managed API 會查詢檢視並呼叫本節中說明的預存程序，以執行許多工作。  
  
## <a name="in-this-section"></a>本節內容  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
 在封裝資料流程中的元件輸出上，加入資料點選。  
  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
 在封裝資料流程中，將資料點選加入至特定的資料流程路徑。  
  
 [catalog.check_schema_version](../../integration-services/system-stored-procedures/catalog-check-schema-version.md)  
 判斷 SSISDB 目錄結構描述與 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 二進位檔 (ISServerExec 和 SQLCLR 組件) 是否相容。  
  
 [catalog.clear_object_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)  
 清除現有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案或封裝儲存在伺服器上的參數值。  
  
 [catalog.configure_catalog &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)  
 藉由將目錄屬性設定為指定值來設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄。  
  
 [catalog.create_environment &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄建立環境。  
  
 [catalog.create_environment_reference &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
 為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案建立環境參考。  
  
 [catalog.create_environment_variable &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中建立環境變數。  
  
 [catalog.create_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中建立執行執行個體。  
  
 [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
 導致執行中的封裝暫停，並建立傾印檔案。  
  
 [catalog.create_folder &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中建立資料夾。  
  
 [catalog.delete_environment &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
 從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的資料夾刪除環境。  
  
 [catalog.delete_environment_reference &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
 從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案刪除環境參考。  
  
 [catalog.delete_environment_variable &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
 從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的環境刪除環境變數。  
  
 [catalog.delete_folder &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
 從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄刪除資料夾。  
  
 [catalog.delete_project &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
 從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的資料夾刪除現有專案。  
  
 [catalog.deny_permission &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md)  
 拒絕 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的安全性實體物件權限。  
  
 [catalog.deploy_project &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
 將專案部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的資料夾，或更新先前已部署的現有專案。  
  
 [catalog.get_parameter_values &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md)  
 從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案和對應封裝解析與擷取預設參數值。  
  
 [catalog.get_project &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
 擷取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 類別目錄中現有專案的屬性。  
  
 [catalog.grant_permission &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
 為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的安全性實體物件授與權限。  
  
 [catalog.move_environment &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
 將環境從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的某個資料夾移動到另一個資料夾。  
  
 [catalog.move_project &#40;&#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-move-project-ssisdb-database.md)  
 將專案從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的某個資料夾移動到另一個資料夾。  
  
 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md)  
 從執行中的元件輸出移除資料點選。  
  
 [catalog.rename_environment &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
 重新命名 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的環境。  
  
 [catalog.rename_folder &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
 重新命名 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的資料夾。  
  
 [catalog.restore_project &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
 將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案還原到舊版。  
  
 [catalog.revoke_permission &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md)  
 撤銷 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的安全性實體物件權限。  
  
 [catalog.set_environment_property &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
 設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的環境屬性。  
  
 [catalog.set_environment_reference_type &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案，設定與現有環境參考相關聯之參考類型和環境名稱。  
  
 [catalog.set_environment_variable_property &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
 設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中環境變數的屬性。  
  
 [catalog.set_environment_variable_protection &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md)  
 設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中環境變數的區分位元。  
  
 [catalog.set_environment_variable_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
 設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中環境變數的值。  
  
 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中執行的執行個體設定參數值。  
  
 [catalog.set_execution_property_override_value](../../integration-services/system-stored-procedures/catalog-set-execution-property-override-value.md)  
 為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中執行的執行個體設定屬性值。  
  
 [catalog.set_folder_description &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
 設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中資料夾的描述。  
  
 [catalog.set_object_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md)  
 設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的參數值。 將值與環境變數建立關聯，或指派常值，在沒有指派其他值的情況下依預設使用。  
  
 [catalog.start_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)  
 啟動在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的執行執行個體。  
  
 [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md)  
 執行 SSISDB 目錄之作業狀態的維護。  
  
 [catalog.stop_operation &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)  
 停止 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的驗證或執行執行個體。  
  
 [catalog.validate_package &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md)  
 以非同步方式驗證 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的封裝。  
  
 [catalog.validate_project &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md)  
 以非同步方式驗證 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案。  
  
[catalog.add_execution_worker &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)   
將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker 新增 Scale Out 中的執行個體。

[catalog.enable_worker_agent &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)   
啟用處理此 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄之 Scale Out Master 的 Scale Out Worker。

[catalog.disable_worker_agent &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)   
停用處理此 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄之 Scale Out Master 的 Scale Out Worker。


