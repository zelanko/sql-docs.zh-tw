---
description: DeleteRecord 方法 (ADO)
title: " (ADO) 的 DeleteRecord 方法 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 94423c36dd89d6ea14ea39b7546ef1a5bef7c620
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444100"
---
# <a name="deleterecord-method-ado"></a>DeleteRecord 方法 (ADO)
刪除 [記錄](../../../ado/reference/ado-api/record-object-ado.md)所表示的實體。  
  
## <a name="syntax"></a>語法  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 **字串**值，包含識別實體的 URL (例如，) 要刪除的檔案或目錄。 如果省略 *Source* 或指定空字串，則會刪除目前 [記錄](../../../ado/reference/ado-api/record-object-ado.md) 所代表的實體。 如果記錄是集合記錄 (**adCollectionRecord**的[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md) ，例如目錄) 所有子系 (例如，也會一併刪除子目錄) 。  
  
 *非同步*  
 選擇性。 **布林**值，若**為 True**，則指定刪除作業非同步。  
  
## <a name="remarks"></a>備註  
 這個 **記錄** 所表示之物件上的作業可能會在此方法完成後失敗。 在呼叫**DeleteRecord**之後，應關閉**記錄**，因為當提供者使用資料來源更新**記錄**時，**記錄**的行為可能會變成無法預測。  
  
 如果從[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)取得此**記錄**，此作業的結果將不會立即反映在**記錄集中**。 藉由關閉並重新開啟記錄集，或執行**記錄集** [Requery](../../../ado/reference/ado-api/requery-method.md)方法、 [Update](../../../ado/reference/ado-api/update-method.md)方法或[Resync](../../../ado/reference/ado-api/resync-method.md)方法來重新整理**記錄集**。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用 [Microsoft OLE DB 提供者進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 [絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO Fields 集合) 的 Delete 方法 ](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 (ADO Parameters 集合) ](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
