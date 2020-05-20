---
title: GetRows 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
author: rothja
ms.author: jroth
ms.openlocfilehash: 3e468e24506425d995320a8729272f87ac64943b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760034"
---
# <a name="getrows-method-ado"></a>GetRows 方法 (ADO)
將[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的多個記錄捕獲到陣列中。  
  
## <a name="syntax"></a>語法  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回其值為二維陣列的**Variant** 。  
  
#### <a name="parameters"></a>參數  
 *資料列*  
 選擇性。 [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)值，表示要取得的記錄數目。 預設值為**adGetRowsRest**。  
  
 *開始*  
 選擇性。 **字串**值或**Variant** ，會評估為要從中開始**GetRows**作業之記錄的書簽。 您也可以使用[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)值。  
  
 *欄位*  
 選擇性。 表示單一功能變數名稱或序數位置的**Variant** ，或功能變數名稱或序數位置數位的陣列。 ADO 只會傳回這些欄位中的資料。  
  
## <a name="remarks"></a>備註  
 使用**GetRows**方法將記錄從**記錄集**複製到二維陣列。 第一個注標會識別欄位，而第二個則會識別記錄號碼。 當**GetRows**方法傳回資料時，*陣列*變數會自動維度為正確的大小。  
  
 如果您未指定*Rows*引數的值，則**GetRows**方法會自動抓取**記錄集**物件中的所有記錄。 如果您要求的記錄數超過可用的數量，則**GetRows**只會傳回可用記錄的數目。  
  
 如果**記錄集**物件支援書簽，您可以在*開始*引數中傳遞該記錄的 [[書簽](../../../ado/reference/ado-api/bookmark-property-ado.md)] 屬性的值，以指定**要在哪個**記錄上開始抓取資料。  
  
 如果您想要限制**GetRows**呼叫傳回的欄位，您可以在*fields*引數中傳遞單一功能變數名稱/數位，或功能變數名稱/數位陣列。  
  
 在您呼叫**GetRows**之後，下一個未讀取的記錄就會成為目前的記錄，否則如果沒有其他記錄， [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性會設定為**True** 。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetRows 方法範例（VB）](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [GetRows 方法範例 (VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
