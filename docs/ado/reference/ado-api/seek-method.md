---
title: 搜尋方法 |Microsoft 文件
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
- Recordset21::Seek
- Recordset21::raw_Seek
helpviewer_keywords:
- Seek method [ADO]
ms.assetid: 129293d2-19d3-4940-bf64-483ee72fb4a1
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59dcdd3426c39449b3d2348218aa7794a75c0474
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="seek-method"></a>搜尋方法
搜尋的索引[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)來快速找出符合指定的值，並變更該資料列目前資料列位置的資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>參數  
 *Parentkeyvalue*  
 陣列**Variant**值。 索引包含一或多個資料行，且此陣列包含要比較每個對應的資料行的值。  
  
 *SeekOption*  
 A [SeekEnum](../../../ado/reference/ado-api/seekenum.md)值，指定要對索引資料行和對應的比較類型*Parentkeyvalue*。  
  
## <a name="remarks"></a>備註  
 使用**搜尋**方法搭配[索引](../../../ado/reference/ado-api/index-property.md)如果基礎提供者在支援索引屬性**資料錄集**物件。 使用[支援](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** 方法，以判斷基礎提供者是否支援**搜尋**，而**Supports(adIndex)** 若要判斷提供者是否支援索引的方法。 (例如， [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)支援**搜尋**和**索引**。)  
  
 如果**搜尋**找不到所需的資料列，沒有任何錯誤發生時，會和資料列位於結尾**資料錄集**。 設定**索引**所要的索引，然後再執行這個方法的屬性。  
  
 只與伺服器端資料指標支援這個方法。 搜尋不支援當**資料錄集**物件的[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性值是**adUseClient**。  
  
 這個方法僅能使用的時機**資料錄集**物件已經開啟與[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值**adCmdTableDirect**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [搜尋方法和索引屬性範例 (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [搜尋方法和索引屬性的範例 （VC + +）](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Index 屬性](../../../ado/reference/ado-api/index-property.md)
