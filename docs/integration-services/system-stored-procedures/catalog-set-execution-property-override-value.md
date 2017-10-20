---
title: "catalog.set_execution_property_override_value |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 37cb3c01-f4c0-4978-8e40-a975456def5a
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 20f2c882a78f5e60931b0152d5877898e1972d0a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetexecutionpropertyoverridevalue"></a>catalog.set_execution_property_override_value
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中執行的執行個體設定屬性值。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.set_execution_property_override_value [ @execution_id = execution_id  
    , [ @property_path = ] property_path  
    , [ @property_value = ] property_value  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>引數  
 [ @execution_id =] *execution_id*  
 執行之執行個體的唯一識別碼。 *Execution_id*是**bigint**。  
  
 [ @property_path =] *property_path*  
 封裝中之屬性的路徑。 *Property_path*是**nvarchar （4000)**。  
  
 [ @property_value =] *property_value*  
 要指派給屬性的覆寫值。 *Property_value*是**nvarchar （max)**。  
  
 [ @sensitive =]*機密*  
 當值為 1 時，屬性為敏感值，而且會在儲存時加密。 當值為 0 時，屬性不是敏感值，而且會儲存為純文字。 *機密*引數是**元**。  
  
## <a name="remarks"></a>備註  
 此程序會執行相同的功能**屬性會覆寫**一節中**進階** 索引標籤**執行封裝**對話方塊。 屬性的路徑衍生自**封裝路徑**「 封裝 」 工作的屬性。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   使用者未具備適當的權限  
  
-   執行識別碼無效  
  
-   屬性路徑無效  
  
-   屬性值的資料類型與屬性的資料類型不符  
  
## <a name="see-also"></a>另請參閱  
 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
  
