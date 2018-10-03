---
title: DeleteRecord 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords:
- DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23c66eb3ca786df27f856539e8bba026d2b1ea71
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674108"
---
# <a name="deleterecord-method-ado"></a>DeleteRecord 方法 (ADO)
刪除所代表的實體[記錄](../../../ado/reference/ado-api/record-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 A**字串**包含識別的實體 （例如，檔案或目錄） 的 URL，要刪除的值。 如果*來源*省略，或者指定空字串，表示由目前的實體[記錄](../../../ado/reference/ado-api/record-object-ado.md)會被刪除。 如果記錄集合記錄 ([RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)的**adCollectionRecord**，例如目錄) 也會刪除所有子系 （例如，子目錄）。  
  
 *非同步處理*  
 選擇性。 A**布林**值，當 **，則為 True**，指定刪除作業為非同步。  
  
## <a name="remarks"></a>備註  
 所表示的物件上的作業**記錄**這個方法完成之後可能會失敗。 之後呼叫**DeleteRecord**，則**記錄**應該關閉，因為行為**記錄**視提供者的更新時無法預期可能會變得**記錄**與資料來源。  
  
 如果這個**記錄**取自於[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，則這項作業的結果不會立即在反映**資料錄集**。 重新整理**Recordset**關閉並重新開啟它，或藉由執行**資料錄集** [Requery](../../../ado/reference/ado-api/requery-method.md)方法，[更新](../../../ado/reference/ado-api/update-method.md)方法，或[Resync](../../../ado/reference/ado-api/resync-method.md)方法。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 <<c0> [ 絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Delete 方法 (ADO Fields 集合)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO Parameters 集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
