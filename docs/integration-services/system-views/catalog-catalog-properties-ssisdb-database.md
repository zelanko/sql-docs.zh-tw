---
title: catalog.catalog_properties (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 12/11/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: e604a382-95c8-4764-b268-742eb5c6d4cf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9b5f7628f0284cb4662f0cf88bff1fd80cb2014e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71295234"
---
# <a name="catalogcatalog_properties-ssisdb-database"></a>catalog.catalog_properties (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄的屬性。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|目錄屬性的名稱。|  
|property_value|**nvarchar(256)**|目錄屬性的值。|  
  
## <a name="remarks"></a>備註  
 這個檢視會顯示每個目錄屬性的資料列。
  
|屬性名稱|描述|  
|-------------------|-----------------|  
|**DEFAULT_EXECUTION_MODE**|套件的全伺服器預設執行模式 - `Server` (0) 或 `Scale Out` (1)。 |
|**ENCRYPTION_ALGORITHM**|用來加密機密資料的加密演算法類型。 支援的值包括：`DES`、`TRIPLE_DES`、`TRIPLE_DES_3KEY`、`DESX`、`AES_128`、`AES_192` 和 `AES_256`。 注意：目錄資料庫必須處於單一使用者模式，才可以變更這個屬性。|
|**IS_SCALEOUT_ENABLED**|當值為 `True` 時，會啟用 SSIS Scale Out 功能。 如果您尚未啟用 Scale Out，則此屬性可能不會出現在檢視中。|
|**MAX_PROJECT_VERSIONS**|單一專案會保留的新專案版本數目。 已啟用版本清除時，會刪除超過這個計數的較舊版本。|  
|**OPERATION_CLEANUP_ENABLED**|當值為 `TRUE` 時，會從目錄中刪除早於 **RETENTION_WINDOW** (天) 的作業詳細資料和作業訊息。 當值為 `FALSE` 時，所有作業詳細資訊和作業訊息都會儲存在目錄中。 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作會執行作業清除。|  
|**RETENTION_WINDOW**|作業詳細資訊和作業訊息儲存在目錄中的天數。 當值為 `-1` 時，保留週期為無限。 注意：如果不想要使用清除，請將 **OPERATION_CLEANUP_ENABLED** 設定為 **FALSE**。|
|**SCHEMA_BUILD**|SSISDB 目錄資料庫結構描述的組建編號。 每當建立或升級 SSISDB 目錄時，就會變更此數字。|
|**SCHEMA_VERSION**|SSISDB 目錄資料庫結構描述的主要版本號碼。 每當建立 SSISDB 目錄或升級主要版本時，就會變更此數字。|
|**VALIDATION_TIMEOUT**|如果驗證沒有在這個屬性指定的秒數中完成，驗證會停止。|  
|**SERVER_CUSTOMIZED_LOGGING_LEVEL**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的預設自訂記錄層次。 如果您尚未建立任何自訂的記錄層次，則此屬性可能不會出現在檢視中。|
|**SERVER_LOGGING_LEVEL**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的預設記錄層級。|
|**SERVER_OPERATION_ENCRYPTION_LEVEL**|當值為 1 (`PER_EXECUTION`) 時，會針對每次「執行」  建立用於保護機密執行參數和執行記錄的憑證和對稱金鍵。 當值為 2 (`PER_PROJECT`) 時，會為每個「專案」  建立憑證和對稱金鑰一次。 如需此屬性的詳細資訊，請參閱適用於 SSIS 預存程序 [catalog.cleanup_server_log](../system-stored-procedures/catalog-cleanup-server-log.md#remarks) 的＜備註＞。|
|**VERSION_CLEANUP_ENABLED**|當值為 `TRUE` 時，目錄中只會儲存 **MAX_PROJECT_VERSIONS** 數目的專案版本，並會刪除所有其他專案版本。 當值為 **FALSE** 時，所有專案版本都會儲存在目錄中。 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作會執行作業清除。|
|||
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
  
