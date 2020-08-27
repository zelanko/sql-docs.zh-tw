---
description: GetRows 方法 (ADO)
title: " (ADO) 的 GetRows 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 666eabf1a375c6a86826bc94600846bd10a0ecfe
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990909"
---
# <a name="getrows-method-ado"></a>GetRows 方法 (ADO)
將 [記錄集](./recordset-object-ado.md) 物件的多筆記錄抓取到陣列中。  
  
## <a name="syntax"></a>語法  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回值為二維陣列的 **Variant** 。  
  
#### <a name="parameters"></a>參數  
 *資料列*  
 選擇性。 [GetRowsOptionEnum](./getrowsoptionenum.md)值，指出要取出的記錄數目。 預設值為 **adGetRowsRest**。  
  
 *啟動*  
 選擇性。 **字串**值或變異數，這個值或**變數**會評估為要從中開始進行**GetRows**作業之記錄的書簽。 您也可以使用 [BookmarkEnum](./bookmarkenum.md) 值。  
  
 *欄位*  
 選擇性。 表示單一功能變數名稱或序數位置的 **Variant** ，或是功能變數名稱或序數位置數位的陣列。 ADO 只會傳回這些欄位中的資料。  
  
## <a name="remarks"></a>備註  
 使用 **GetRows** 方法將記錄從 **記錄集** 複製到二維陣列。 第一個注標會識別欄位，第二個則會識別記錄號碼。 當**GetRows**方法傳回資料時，*陣列*變數會自動維度為正確的大小。  
  
 如果您未指定 *Rows* 引數的值， **GetRows** 方法會自動抓取 **記錄集** 物件中的所有記錄。 如果您要求的記錄數目超過可用的數量，則 **GetRows** 只會傳回可用記錄的數目。  
  
 如果**記錄集**物件支援書簽，您可以藉由在*Start*引數中傳遞該記錄的 [[書簽](./bookmark-property-ado.md)] 屬性的值，指定要在哪一個記錄上，讓**GetRows**方法開始取出資料。  
  
 如果您想要限制 **GetRows** 呼叫傳回的欄位，您可以在 *fields* 引數中傳遞單一功能變數名稱/數位或功能變數名稱/數位的陣列。  
  
 在您呼叫 **GetRows**之後，下一個未讀取的記錄就會變成目前的記錄，如果沒有其他記錄，則 [EOF](./bof-eof-properties-ado.md) 屬性會設定為 **True** 。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 GetRows 方法範例 ](./getrows-method-example-vb.md)   
 [GetRows 方法範例 (VC++)](./getrows-method-example-vc.md)