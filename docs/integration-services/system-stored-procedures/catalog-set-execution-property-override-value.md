---
title: catalog.set_execution_property_override_value | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 37cb3c01-f4c0-4978-8e40-a975456def5a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3a009f23b1c6ca3520793a7c1f947afe0ff0516a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912824"
---
# <a name="catalogset_execution_property_override_value"></a>catalog.set_execution_property_override_value 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中執行的執行個體設定屬性值。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.set_execution_property_override_value [ @execution_id = execution_id  
    , [ @property_path = ] property_path  
    , [ @property_value = ] property_value  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>引數  
 [ @execution_id = ] *execution_id*  
 執行之執行個體的唯一識別碼。 *execution_id* 是 **bigint**。  
  
 [ @property_path = ] *property_path*  
 封裝中之屬性的路徑。 *property_path* 是 **nvarchar(4000)** 。  
  
 [ @property_value = ] *property_value*  
 要指派給屬性的覆寫值。 *property_value* 是 **nvarchar(max)** 。  
  
 [ @sensitive = ] *sensitive*  
 當值為 1 時，屬性為敏感值，而且會在儲存時加密。 當值為 0 時，屬性不是敏感值，而且會儲存為純文字。 *sensitive* 引數是 **bit**。  
  
## <a name="remarks"></a>備註  
 這個程序會與 [執行封裝] 對話方塊之 [進階] 索引標籤中的 [屬性覆寫] 區段執行相同的功能。 屬性的路徑衍生自封裝工作的 [封裝路徑]  屬性。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   使用者未具備適當的權限  
  
-   執行識別碼無效  
  
-   屬性路徑無效  
  
-   屬性值的資料類型與屬性的資料類型不符  
  
## <a name="see-also"></a>另請參閱  
 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
  
