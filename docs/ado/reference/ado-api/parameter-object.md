---
title: 參數物件 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameter
helpviewer_keywords:
- Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3a3bd9f746c53a046644dff8840a09024addb7c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-object"></a>Parameter 物件
代表參數或相關聯的引數[命令](../../../ado/reference/ado-api/command-object-ado.md)物件會根據參數型的查詢或預存程序。  
  
## <a name="remarks"></a>備註  
 許多提供者支援參數化的命令。 這些命令所需的動作定義的一次，但變數 （或參數） 用來改變命令的一些詳細資料。 例如，SQL SELECT 陳述式可以使用參數，定義 WHERE 子句，來定義資料行名稱排序依據子句的另一個符合的條件。  
  
 **參數**物件代表具有參數化查詢時，相關聯的參數或輸入/輸出引數和傳回值的預存程序。 依據其功能的提供者、 某些集合、 方法或屬性的**參數**物件可能無法使用。  
  
 使用集合、 方法和屬性的**參數**物件，您可以執行下列：  
  
-   設定或傳回的參數名稱[名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性。  
  
-   設定或傳回的參數值[值](../../../ado/reference/ado-api/value-property-ado.md)屬性。 **值**是預設屬性**參數**物件。  
  
-   設定或傳回參數特性與[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)，[方向](../../../ado/reference/ado-api/direction-property.md)，[精確度](../../../ado/reference/ado-api/precision-property-ado.md)， [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)， [大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)，和[類型](../../../ado/reference/ado-api/type-property-ado.md)屬性。  
  
-   將長二進位或字元資料傳遞至具有參數[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)方法。  
  
-   使用存取提供者專屬屬性[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 如果您知道名稱，與相關聯的參數屬性要呼叫的預存程序或參數化的查詢，您可以使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法來建立**參數**物件使用適當的屬性設定和使用[附加](../../../ado/reference/ado-api/append-method-ado.md)方法將其新增至[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 這可讓您設定和傳回參數值，而不必呼叫[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法**參數**提供者，從擷取的參數資訊的集合可能需要大量資源的作業。  
  
 **參數**物件不是安全的。  
  
 本章節包含下列主題。  
  
-   [參數物件屬性、 方法和事件](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [命令物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [參數集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
