---
title: 欄位物件 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field
helpviewer_keywords:
- Field object [ADO]
ms.assetid: b10a72fc-3c4b-4186-a70b-993dc9f7a092
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b815da825f777b51a43a90af26eba955050b785
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278467"
---
# <a name="field-object"></a>Field 物件
代表具有通用的資料類型的資料行。  
  
## <a name="remarks"></a>備註  
 每個**欄位**物件對應中的資料行[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 您使用[值](../../../ado/reference/ado-api/value-property-ado.md)屬性**欄位**設定或傳回目前的記錄資料的物件。 依據其功能提供者會公開，某些集合、 方法或屬性的**欄位**物件可能無法使用。  
  
 使用集合、 方法和屬性的**欄位**物件，您可以執行下列：  
  
-   傳回具有的欄位名稱[名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性。  
  
-   檢視或變更的欄位中的資料**值**屬性。 **值**是預設屬性**欄位**物件。  
  
-   傳回具有欄位的基本特性[類型](../../../ado/reference/ado-api/type-property-ado.md)，[精確度](../../../ado/reference/ado-api/precision-property-ado.md)，和[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)屬性。  
  
-   傳回具有欄位的宣告的大小[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)屬性。  
  
-   傳回具有給定欄位中的實際資料大小[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)屬性。  
  
-   判斷哪些類型的功能支援具有給定欄位[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性和[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
-   管理包含長的二進位或字元長度的資料與欄位的值[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)和[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)方法。  
  
-   如果提供者支援批次更新，解決不一致的欄位值在批次更新與[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)和[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)屬性。  
  
 所有中繼資料屬性 (**名稱**，**類型**， **DefinedSize**，**精確度**，和**NumericScale**) 可用才能開啟**欄位**物件的**資料錄集**。 設定在當時適用於以動態方式建構表單。  
  
 本章節包含下列主題。  
  
-   [欄位的物件屬性、 方法和事件](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [欄位集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
