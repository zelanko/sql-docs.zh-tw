---
title: "catalog.set_customized_logging_level_description |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 6ceaa39f-2439-457b-b99f-f12d88a1be32
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3899e02c6b1eaa2cc76ad4411d9be3aded817728
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetcustomizedloggingleveldescription"></a>catalog.set_customized_logging_level_description
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  變更現有的自訂的記錄層級的描述。 如需自訂的記錄層級的詳細資訊，請參閱[Integration Services &#40;SSIS &#41;記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.set_customized_logging_level_description [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
```  
  
## <a name="arguments"></a>引數  
 [ @level_name =] *l*  
 名稱的現有自訂記錄層級。  
  
 *l*是**nvarchar （128)**。  
  
 [ @level_description =] *level_description*  
 指定的新描述自訂記錄層級。  
  
 *Level_description*是**nvarchar （1024)**。  
  
## <a name="remarks"></a>備註  
  
## <a name="return-codes"></a>傳回碼  
 0 (成功)  
  
 當預存程序失敗時，會擲回錯誤。  
  
## <a name="result-set"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   **ssis_admin** 資料庫角色中的成員資格  
  
-   **sysadmin** 伺服器角色中的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致預存程序失敗的情況。  
  
-   使用者沒有必要的權限。  
  
  

