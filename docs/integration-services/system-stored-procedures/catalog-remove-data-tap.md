---
title: catalog.remove_data_tap | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b77db3e6-478c-441a-a838-82c4de750275
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: abbb37dee6cf17af196679ed2136cf792ce49f3f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610296"
---
# <a name="catalogremovedatatap"></a>catalog.remove_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  從執行中的元件輸出移除資料點選。 資料點選的唯一識別碼與執行的執行個體相關聯。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.remove_data_tap [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>引數  
 [ @data_tap_id = ] *data_tap_id*  
 使用 catalog.add_data_tap 預存程序來建立之資料點選的唯一識別碼。 *data_tap_id* 是 **bigint**。  
  
## <a name="remarks"></a>Remarks  
 如果封裝包含多個具有相同名稱的資料流程工作，則會將資料點選加入具有給定名稱的第一個資料流程工作。  
  
## <a name="return-codes"></a>傳回碼  
 0 (成功)  
  
 當預存程序失敗時，會擲回錯誤。  
  
## <a name="result-set"></a>結果集  
 None  
  
## <a name="remarks"></a>Remarks  
 若要移除資料點選，執行的執行個體必須處於已建立狀態 ([catalog.operations &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 檢視之 [狀態] 資料行中的值為 1)。  
  
## <a name="permissions"></a>[權限]  
 這個預存程序需要下列其中一個權限：  
  
-   執行的執行個體之 MODIFY 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致預存程序失敗的情況。  
  
-   使用者沒有 MODIFY 權限。  
  
## <a name="see-also"></a>另請參閱  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)   
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
