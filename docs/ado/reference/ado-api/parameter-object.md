---
title: Parameter 物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameter
helpviewer_keywords:
- Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15df27e3dc48decf743a78dd4d147a22dc7cf276
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931669"
---
# <a name="parameter-object"></a>Parameter 物件
根據參數化查詢或預存程式，表示與[命令](../../../ado/reference/ado-api/command-object-ado.md)物件相關聯的參數或引數。  
  
## <a name="remarks"></a>備註  
 許多提供者都支援參數化命令。 這些是所需動作定義一次的命令，但變數（或參數）是用來改變命令的一些詳細資料。 例如，SQL SELECT 語句可以使用參數來定義 WHERE 子句的比對準則，另一個則是用來定義排序依據子句的資料行名稱。  
  
 **參數**物件代表與參數化查詢相關聯的參數，或 in/out 引數和預存程式的傳回值。 視提供者的功能而定，某些集合、方法或**參數**物件的屬性可能無法使用。  
  
 使用**參數**物件的集合、方法和屬性，您可以執行下列動作：  
  
-   設定或傳回具有[name](../../../ado/reference/ado-api/name-property-ado.md)屬性之參數的名稱。  
  
-   使用[value](../../../ado/reference/ado-api/value-property-ado.md)屬性來設定或傳回參數的值。 **Value**是**參數**物件的預設屬性。  
  
-   使用[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)、[方向](../../../ado/reference/ado-api/direction-property.md)、有效[位數](../../../ado/reference/ado-api/precision-property-ado.md)、 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)、[大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)和[類型](../../../ado/reference/ado-api/type-property-ado.md)屬性來設定或傳回參數特性。  
  
-   使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)方法將長二進位或字元資料傳遞至參數。  
  
-   使用[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合存取提供者特有的屬性。  
  
 如果您知道與您要呼叫的預存程式或參數化查詢相關聯之參數的名稱和屬性，您可以使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法來建立具有適當屬性設定的**參數**物件，並使用[Append](../../../ado/reference/ado-api/append-method-ado.md)方法將它們新增至[parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 這可讓您設定和傳回參數值，而不需要在**Parameters**集合上呼叫[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法，以從提供者（可能是需要大量資源的作業）取得參數資訊。  
  
 **參數**物件不安全，無法進行腳本處理。  
  
 本章節包含下列主題。  
  
-   [Parameter 物件屬性、方法和事件](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Command 物件（ADO）](../../../ado/reference/ado-api/command-object-ado.md)   
 [CreateParameter 方法（ADO）](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameters 集合（ADO）](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
