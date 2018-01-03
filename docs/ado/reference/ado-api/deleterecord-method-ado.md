---
title: "DeleteRecord 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords: DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eedc8d14c94ec89554651cdfce03af0eb63315cf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="deleterecord-method-ado"></a>DeleteRecord 方法 (ADO)
刪除所代表的實體[記錄](../../../ado/reference/ado-api/record-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 A**字串**值，包含 URL 識別 （例如，檔案或目錄） 的實體被刪除。 如果*來源*省略或空字串，表示由目前的實體指定[記錄](../../../ado/reference/ado-api/record-object-ado.md)被刪除。 如果記錄集合記錄 ([RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)的**adCollectionRecord**，例如目錄) 所有的子系 （例如，是子目錄） 也將一併刪除。  
  
 *非同步*  
 選擇性。 A**布林**值，當**True**，指定刪除作業是非同步。  
  
## <a name="remarks"></a>備註  
 物件所代表的作業**記錄**這個方法完成之後，可能會失敗。 在呼叫**DeleteRecord**、**記錄**應該關閉，因為行為的**記錄**變得無法預測視提供者會更新時**記錄**與資料來源。  
  
 如果這個**記錄**已經從取得[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，則此作業的結果不會立即在反映**資料錄集**。 重新整理**資料錄集**地關閉並重新開啟它，或藉由執行**資料錄集** [Requery](../../../ado/reference/ado-api/requery-method.md)方法，[更新](../../../ado/reference/ado-api/update-method.md)方法，或[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>請參閱  
 [Delete 方法 （ADO 欄位集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 參數集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
