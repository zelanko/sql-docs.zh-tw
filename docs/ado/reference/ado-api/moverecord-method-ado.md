---
title: MoveRecord 方法 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3c6361dca137a27c5b54149fd400ee5cd29d9160
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="moverecord-method-ado"></a>MoveRecord 方法 (ADO)
移動所代表的實體[記錄](../../../ado/reference/ado-api/record-object-ado.md)到另一個位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 A**字串**值，包含 URL 識別**記錄**可移動。 如果*來源*省略或空字串，所表示的物件指定**記錄**移動。 例如，如果**記錄**代表的檔案，檔案的內容會移至所指定的位置*目的地*。  
  
 *目的地*  
 選擇性。 A**字串**值，其中包含指定位置的 URL 位置*來源*會移動。  
  
 *UserName*  
 選擇性。 A**字串**值，其中包含的使用者識別碼，如有需要授與存取權*目的地*。  
  
 *密碼*  
 選擇性。 A**字串**其中包含的密碼，如有需要驗證*UserName*。  
  
 *選項。*  
 選擇性。 A [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)值，其預設值是**adMoveUnspecified**。 指定此方法的行為。  
  
 *非同步*  
 選擇性。 A**布林**值，當**True**，指定此作業應該是非同步。  
  
## <a name="return-value"></a>傳回值  
 A**字串**值。 一般而言，值*目的地*傳回。 不過，傳回的實際值會提供者而異。  
  
## <a name="remarks"></a>備註  
 值*來源*和*目的地*不能相同; 否則就會發生執行階段錯誤。 至少必須在不同的伺服器、 路徑和資源的名稱。  
  
 使用網際網路發行的提供者移動的檔案，這個方法會更新所有正在移動，除非另有指定的檔案中的超文字連結*選項*。 如果這個方法會失敗*目的地*識別現有的物件 （例如，檔案或目錄），除非**adMoveOverWrite**指定。  
  
> [!NOTE]
>  使用**adMoveOverWrite**明智選項。 例如，將檔案移至目錄時，指定這個選項將刪除目錄，並取代檔案。  
  
 某些屬性**記錄**物件，例如[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)屬性，將不會更新，這項作業完成之後。 重新整理**記錄**物件的屬性，透過關閉**記錄**，然後重新開啟它的位置，其中已移動的檔案或目錄的 url。  
  
 如果這個**記錄**已經從取得[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，已移動的檔案或目錄的新位置不會立即在反映**資料錄集**。 重新整理**資料錄集**地關閉並重新開啟它。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Move 方法 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)
