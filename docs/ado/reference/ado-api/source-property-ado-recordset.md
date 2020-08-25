---
description: Source 屬性 (ADO Recordset)
title: 來源屬性 (ADO 記錄集) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 29ce12027267918822ed49185f06ab28a6448190
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777397"
---
# <a name="source-property-ado-recordset"></a>Source 屬性 (ADO Recordset)
表示 [記錄集](./recordset-object-ado.md) 物件的資料來源。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定**字串**值或[命令](./command-object-ado.md)物件參考;只傳回表示**記錄集**來源的**字串**值。  
  
## <a name="remarks"></a>備註  
 您可以使用 [ **來源** ] 屬性，使用下列其中一種方法來指定 **記錄集** 物件的資料來源： **命令** 物件變數、SQL 語句、預存程式或資料表名稱。  
  
 如果您將**Source**屬性設定為**Command**物件，**記錄集**物件的[ActiveConnection](./activeconnection-property-ado.md)屬性將會繼承指定**命令**物件的**ActiveConnection**屬性值。 但是，讀取**Source**屬性不會傳回**命令**物件;相反地，它會傳回您設定**Source**屬性的**命令**物件之[CommandText](./commandtext-property-ado.md)屬性。  
  
 如果**來源**屬性是 SQL 語句、預存程式或資料表名稱，您可以使用[Open](./open-method-ado-recordset.md)方法呼叫傳遞適當的*選項*引數，以優化效能。  
  
 [ **來源** ] 屬性是已關閉 **記錄集** 物件的讀取/寫入，而開啟的 **記錄集** 物件是唯讀的。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Source 屬性範例 (VB) ](./source-property-example-vb.md)   
 [ (ADO Error) 的 Source 屬性 ](./source-property-ado-error.md)   
 [Source 屬性 (ADO Record)](./source-property-ado-record.md)