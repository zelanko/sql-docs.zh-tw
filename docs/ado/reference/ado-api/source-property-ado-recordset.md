---
title: 來源屬性 (ADO Recordset) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 59a043b6258de83986e447c87209fa781a1ae352
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711112"
---
# <a name="source-property-ado-recordset"></a>Source 屬性 (ADO Recordset)
表示的資料來源[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定組**字串**值或[命令](../../../ado/reference/ado-api/command-object-ado.md)物件參考，只會傳回**字串**值，指出來源**資料錄集**。  
  
## <a name="remarks"></a>備註  
 使用**來源**屬性，以指定的資料來源**Recordset**物件使用下列其中之一：**命令**物件變數的 SQL 陳述式、 預存程序中，或資料表名稱。  
  
 如果您設定**來源**屬性設**命令**物件[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性**資料錄集**物件就會繼承值**ActiveConnection**屬性指定**命令**物件。 不過，讀取**來源**屬性不會傳回**命令**物件; 相反地，它會傳回[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性**命令**要用以設定的物件**來源**屬性。  
  
 如果**來源**屬性為 SQL 陳述式、 預存程序中或資料表名稱時，您可以藉由將適當的傳遞最佳化效能*選項*引數與[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法呼叫。  
  
 **來源**屬性是讀取/寫入，如關閉**Recordset**物件且為唯讀狀態開啟**資料錄集**物件。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Source 屬性範例 (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [來源屬性 (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source 屬性 (ADO 記錄)](../../../ado/reference/ado-api/source-property-ado-record.md)
