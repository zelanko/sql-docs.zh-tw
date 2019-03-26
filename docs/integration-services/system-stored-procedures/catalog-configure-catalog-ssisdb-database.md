---
title: catalog.configure_catalog (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b093d11e0a54b9e2c744358de82f7d5b09e7c33
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58274645"
---
# <a name="catalogconfigurecatalog-ssisdb-database"></a>catalog.configure_catalog (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  藉由將目錄屬性設定為指定值來設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄。  
  
## <a name="syntax"></a>語法  
  
```sql
catalog.configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>引數  
 [ @property_name = ] *property_name*  
 目錄屬性的名稱。 *property_name* 是 **nvarchar(255)**。 如需可用屬性的詳細資訊，請參閱 [catalog.catalog_properties &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)。  
  
 [ @property_value = ] *property_value*  
 目錄屬性的值。 *property_value* 是 **nvarchar(255)**。 如需屬性值的詳細資訊，請參閱 [catalog.catalog_properties &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>Remarks  
 這個預存程序會判斷 *property_value* 對每個 *property_name* 是否有效。  
  
 這個預存程序只可以在沒有作用中執行 (例如暫止、已佇列、執行中與已暫停的執行) 時執行。  
  
 正在設定目錄時，所有其他目錄預存程序都會失敗，並出現錯誤訊息「目前正在設定伺服器」。
  
 設定目錄時，項目會寫入作業記錄檔。  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   屬性不存在  
  
-   屬性值無效  
  
  
