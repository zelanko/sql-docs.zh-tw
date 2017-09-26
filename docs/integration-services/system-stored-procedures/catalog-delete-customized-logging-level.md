---
title: "catalog.delete_customized_logging_level |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 0aec1e34-f30b-4e5f-bba1-c26665cf2da6
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a2c53009bfbd2f0876d4cf0a01cf8fa2b5bc738e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeletecustomizedlogginglevel"></a>catalog.delete_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  刪除現有的自訂的記錄層級。 如需自訂的記錄層級的詳細資訊，請參閱[Integration Services &#40;SSIS &#41;記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="syntax"></a>語法  
  
```tsql  
delete_customized_logging_level [ @level_name = ] level_name  
  
```  
  
## <a name="arguments"></a>引數  
 [ @level_name =] *l*  
 名稱的現有自訂記錄層級刪除。  
  
 *l*是**nvarchar （128)**。  
  
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
  
  
