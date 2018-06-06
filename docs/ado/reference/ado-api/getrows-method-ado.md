---
title: GetRows 方法 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efe7a21a26e99d089c64fcd3a627c693c5f7de09
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getrows-method-ado"></a>GetRows 方法 (ADO)
擷取的多筆記錄[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件陣列。  
  
## <a name="syntax"></a>語法  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**Variant**其值是二維陣列。  
  
#### <a name="parameters"></a>參數  
 *資料列*  
 選擇性。 A [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)值，指出要擷取的記錄數目。 預設值是**adGetRowsRest**。  
  
 *啟動*  
 選擇性。 A**字串**值或**Variant**會評估為書籤記錄從中**GetRows**應該開始的作業。 您也可以使用[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)值。  
  
 *欄位*  
 選擇性。 A **Variant**表示的單一欄位名稱或序數位置或欄位名稱或序數位置的數字的陣列。 ADO 會傳回這些欄位中的資料。  
  
## <a name="remarks"></a>備註  
 使用**GetRows**方法來複製資料的來源**資料錄集**成二維陣列。 第一個註標識別欄位，以及第二個識別記錄號碼。 *陣列*變數自動建立的正確維度時**GetRows**方法傳回的資料。  
  
 如果您未指定的值*列*引數， **GetRows**方法自動擷取中的所有記錄**資料錄集**物件。 如果您要求更多的記錄超過可用， **GetRows**傳回的可用的記錄數目。  
  
 如果**資料錄集**物件支援書籤，您可以指定在哪一筆記錄**GetRows**方法應該由此開始傳遞該記錄的值中擷取資料[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)屬性*啟動*引數。  
  
 如果您想要限制的欄位， **GetRows**呼叫傳回時，您可以在單一欄位名稱數目或欄位名稱/中的數字的陣列傳遞*欄位*引數。  
  
 在您呼叫後**GetRows**下, 一個未閱讀的記錄會變成目前的記錄，或[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性設定為**True**如果沒有更多的記錄。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetRows 方法範例 (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [GetRows 方法範例 (VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
