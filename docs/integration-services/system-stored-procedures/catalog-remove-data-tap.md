---
title: "catalog.remove_data_tap |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b77db3e6-478c-441a-a838-82c4de750275
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2f2c9b5d9333c201120e5f3a3e392c59012a8ac7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogremovedatatap"></a>catalog.remove_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  從執行中的元件輸出移除資料點選。 資料點選的唯一識別碼與執行的執行個體相關聯。  
  
## <a name="syntax"></a>語法  
  
```tsql  
remove_data_tap [ @data_tap_id = ] data_tap_id  
  
```  
  
## <a name="arguments"></a>引數  
 [ @data_tap_id =] *data_tap_id*  
 使用 catalog.add_data_tap 預存程序來建立之資料點選的唯一識別碼。 *Data_tap_id*是**bigint**。  
  
## <a name="remarks"></a>備註  
 如果封裝包含多個具有相同名稱的資料流程工作，則會將資料點選加入具有給定名稱的第一個資料流程工作。  
  
## <a name="return-codes"></a>傳回碼  
 0 (成功)  
  
 當預存程序失敗時，會擲回錯誤。  
  
## <a name="result-set"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 若要移除資料點選，執行的執行個體必須是處於已建立狀態 (1 中的值**狀態**資料行[catalog.operations &#40;SSISDB 資料庫 &#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)檢視)。  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   執行的執行個體之 MODIFY 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致預存程序失敗的情況。  
  
-   使用者沒有 MODIFY 權限。  
  
## <a name="see-also"></a>另請參閱  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)   
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
