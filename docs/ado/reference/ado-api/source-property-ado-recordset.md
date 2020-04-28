---
title: Source 屬性（ADO Recordset） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::putref_Source
- Recordset15::Source
- Recordset15::PutSource
- Recordset15::get_Source
- Recordset15::GetSource
- Recordset15::PutRefSource
- Recordset15::put_Source
helpviewer_keywords:
- Source property [ADO Recordset]
ms.assetid: a05ba2c9-2821-4343-8607-4de9b764ec91
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f6ac84445272ae3657d4e25691dbbf150f32c5d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67930926"
---
# <a name="source-property-ado-recordset"></a>Source 屬性 (ADO Recordset)
表示[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的資料來源。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定**字串**值或[命令](../../../ado/reference/ado-api/command-object-ado.md)物件參考;只傳回表示**記錄集**來源的**字串**值。  
  
## <a name="remarks"></a>備註  
 使用 [**來源**] 屬性，即可使用下列其中一種方法來指定**記錄集**物件的資料來源：**命令**物件變數、SQL 語句、預存程式或資料表名稱。  
  
 如果您將**Source**屬性設定為**Command**物件，則**記錄集**物件的[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性將會繼承所指定**命令**物件的**ActiveConnection**屬性值。 不過，讀取**Source**屬性並不會傳回**Command**物件;相反地，它會傳回您設定**Source**屬性之**Command**物件的[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性。  
  
 如果**Source**屬性是 SQL 語句、預存程式或資料表名稱，您可以藉由使用[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法呼叫傳遞適當的*選項*引數，將效能優化。  
  
 對於已關閉的**記錄集**物件， **Source**屬性是讀取/寫入，而對於開啟的**記錄集**物件，則是唯讀的。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Source 屬性範例（VB）](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [Source 屬性（ADO Error）](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source 屬性 (ADO Record)](../../../ado/reference/ado-api/source-property-ado-record.md)
