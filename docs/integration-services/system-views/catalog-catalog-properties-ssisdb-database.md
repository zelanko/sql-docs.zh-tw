---
title: "catalog.catalog_properties （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: e604a382-95c8-4764-b268-742eb5c6d4cf
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ca3d5da05126d5b71bf6d714f9e8449f9f5c8335
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcatalogproperties-ssisdb-database"></a>catalog.catalog_properties (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄的屬性。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|目錄屬性的名稱。|  
|property_value|**nvarchar(256)**|目錄屬性的值。|  
  
## <a name="remarks"></a>備註  
 這個檢視會顯示每個目錄屬性的資料列。 這個檢視會顯示的屬性包括：  
  
|屬性名稱|Description|  
|-------------------|-----------------|  
|**ENCRYPTION_ALGORITHM**|用來加密機密資料的加密演算法類型。 支援的值包括：`DES`、`TRIPLE_DES`、`TRIPLE_DES_3KEY`、`DESX`、`AES_128`、`AES_192` 和 `AES_256`。 注意：目錄資料庫必須處於單一使用者模式，才可以變更這個屬性。|  
|**MAX_PROJECT_VERSIONS**|單一專案將會保留的新專案版本數目。 已啟用版本清除時，會刪除超過這個計數的較舊版本。|  
|**OPERATION_CLEANUP_ENABLED**|當這個值是`TRUE`，作業詳細資料和作業訊息超過**將 RETENTION_WINDOW** （天） 會從目錄中刪除。 當值為 `FALSE` 時，所有作業詳細資訊和作業訊息都會儲存在目錄中。 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作會執行作業清除。|  
|**RETENTION_WINDOW**|作業詳細資訊和作業訊息儲存在目錄中的天數。 當值為 `-1` 時，保留週期為無限。 注意： 如果您想要使用不清除，設定**OPERATION_CLEANUP_ENABLED**至**FALSE**。|  
|**VALIDATION_TIMEOUT**|如果驗證沒有在這個屬性指定的秒數中完成，驗證將會停止。|  
|**VERSION_CLEANUP_ENABLED**|當這個值是`TRUE`，則只**MAX_PROJECT_VERSIONS**專案版本數目會儲存在目錄和所有其他專案版本都會被刪除。 當這個值是**FALSE**，所有專案版本會都儲存在目錄中。 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作會執行作業清除。|  
|**SERVER_LOGGING_LEVEL**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的預設記錄層級。|  
  
## <a name="permissions"></a>Permissions  
 這個檢視需要下列其中一個權限：  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
  
