---
title: "catalog.configure_catalog （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 15bec231bf1de825cea952e07827074d56751386
ms.contentlocale: zh-tw
ms.lasthandoff: 10/20/2017

---
# <a name="catalogconfigurecatalog-ssisdb-database"></a>catalog.configure_catalog (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  藉由將目錄屬性設定為指定值來設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄。  
  
## <a name="syntax"></a>語法  
  
```sql
catalog.configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>引數  
 [ @property_name =] *property_name*  
 目錄屬性的名稱。 *Property_name*是**nvarchar （255)**。 如需有關可用屬性的詳細資訊，請參閱[catalog.catalog_properties &#40;SSISDB 資料庫 &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
 [ @property_value =] *property_value*  
 目錄屬性的值。 *Property_value*是**nvarchar （255)**。 如需有關屬性值的詳細資訊，請參閱[catalog.catalog_properties &#40;SSISDB 資料庫 &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 這個預存程序會判斷是否*property_value*適用於每個*property_name*。  
  
 這個預存程序只可以在沒有作用中執行 (例如暫止、已佇列、執行中與已暫停的執行) 時執行。  
  
 設定目錄時，所有其他目錄預存程序都會失敗並出現錯誤訊息"目前正在設定伺服器。 」
  
 設定目錄時，項目會寫入作業記錄檔。  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   屬性不存在  
  
-   屬性值無效  
  
  

