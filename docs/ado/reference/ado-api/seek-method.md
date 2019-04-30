---
title: 搜尋方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Seek
- Recordset21::raw_Seek
helpviewer_keywords:
- Seek method [ADO]
ms.assetid: 129293d2-19d3-4940-bf64-483ee72fb4a1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89b82d6efe87cec6643d68837447ed64a6f69059
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63314699"
---
# <a name="seek-method"></a>Seek 方法
搜尋的索引[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)來快速尋找符合指定的值，並變更該資料列目前的資料列位置的資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>參數  
 *KeyValues*  
 陣列**Variant**值。 索引是由一或多個資料行所組成，陣列會包含要比較每個對應的資料行的值。  
  
 *SeekOption*  
 A [SeekEnum](../../../ado/reference/ado-api/seekenum.md)值，指定要進行索引的資料行與對應之間的比較類型*Parentkeyvalue*。  
  
## <a name="remarks"></a>備註  
 使用**Seek**方法搭配[Index](../../../ado/reference/ado-api/index-property.md)屬性，如果基礎提供者支援上的索引**資料錄集**物件。 使用[支援](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** 方法，以判斷基礎的提供者是否支援**搜尋**，而**Supports(adIndex)** 若要判斷提供者是否支援索引的方法。 (例如[OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)支援**Seek**並**索引**。)  
  
 如果**Seek**尋找所需的資料列，沒有任何錯誤發生時，會和資料列位於結尾**資料錄集**。 設定**Index**所要的索引，然後再執行這個方法的屬性。  
  
 只有伺服器端資料指標才支援這個方法。 搜尋不支援在當**Recordset**物件的[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性值是**adUseClient**。  
  
 這個方法只能時使用**資料錄集**物件使用開啟[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)的值**adCmdTableDirect**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Seek 方法和 Index 屬性範例 (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Seek 方法和 Index 屬性範例 （VC + +）](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Index 屬性](../../../ado/reference/ado-api/index-property.md)
