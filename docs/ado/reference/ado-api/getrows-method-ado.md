---
title: GetRows 方法 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65d346cb9394613a92f95f7466e429b10c54b1a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027943"
---
# <a name="getrows-method-ado"></a>GetRows 方法 (ADO)
擷取的多筆記錄[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)成陣列的物件。  
  
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
 選擇性。 A**字串**值，或**Variant**評估為書籤記錄從中**GetRows**作業應該開始。 您也可以使用[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)值。  
  
 *欄位*  
 選擇性。 A **Variant**表示的單一欄位名稱或序數位置或欄位名稱或序數位置的數字的陣列。 ADO 會傳回這些欄位中的資料。  
  
## <a name="remarks"></a>備註  
 使用**GetRows**方法來複製資料的來源**資料錄集**的二維陣列。 第一個註標識別欄位，第二個識別的資料錄數目。 *陣列*變數會自動設定為正確大小的時機**GetRows**方法傳回的資料。  
  
 如果您未指定的值*資料列*引數**GetRows**方法會自動擷取中的所有記錄**資料錄集**物件。 如果您要求可供使用，過多的記錄**GetRows**傳回只有可用的記錄數目。  
  
 如果**Recordset**物件支援書籤，您可以指定在哪一筆記錄**GetRows**方法應該開始擷取資料，將該記錄的值傳遞[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)中的屬性*啟動*引數。  
  
 如果您想要限制欄位所**GetRows**呼叫傳回時，您可以將單一欄位名稱/數字或欄位名稱/數字陣列中的傳遞*欄位*引數。  
  
 在您呼叫後**GetRows**下, 一個未閱讀的記錄會變成目前的記錄，或[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性設定為**True**如果沒有更多的記錄。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetRows 方法範例 (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [GetRows 方法範例 (VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
