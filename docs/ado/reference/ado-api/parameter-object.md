---
description: Parameter 物件
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
author: rothja
ms.author: jroth
ms.openlocfilehash: eac5abf388644cff05c4a3a81955f025c65dd7aa
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773407"
---
# <a name="parameter-object"></a>Parameter 物件
根據參數化查詢或預存程式，表示與 [命令](./command-object-ado.md) 物件相關聯的參數或引數。  
  
## <a name="remarks"></a>備註  
 許多提供者支援參數化命令。 這些命令只會定義所需的動作一次，但變數 (或參數) 用來改變命令的部分詳細資料。 例如，SQL SELECT 語句可以使用參數來定義 WHERE 子句的比對準則，並使用另一個來定義 SORT BY 子句的資料行名稱。  
  
 **參數** 物件代表與參數化查詢相關聯的參數，或是 in/out 引數和預存程式的傳回值。 視提供者的功能而定，可能無法使用 **參數** 物件的某些集合、方法或屬性。  
  
 使用 **參數** 物件的集合、方法和屬性，您可以執行下列動作：  
  
-   使用 [name](./name-property-ado.md) 屬性來設定或傳回參數的名稱。  
  
-   使用 [value](./value-property-ado.md) 屬性設定或傳回參數的值。 **值** 是 **參數** 物件的預設屬性。  
  
-   使用 [屬性](./attributes-property-ado.md)、 [方向](./direction-property.md)、有效 [位數](./precision-property-ado.md)、 [NumericScale](./numericscale-property-ado.md)、 [大小](./size-property-ado-parameter.md)和 [類型](./type-property-ado.md) 屬性來設定或傳回參數特性。  
  
-   使用 [AppendChunk](./appendchunk-method-ado.md) 方法將長二進位或字元資料傳遞給參數。  
  
-   使用 [Properties](./properties-collection-ado.md) 集合存取提供者特有的屬性。  
  
 如果您知道您想要呼叫之預存程式或參數化查詢相關聯之參數的名稱和屬性，您可以使用 [CreateParameter](./createparameter-method-ado.md) 方法，以適當的屬性設定來建立 **參數** 物件，並使用 [Append](./append-method-ado.md) 方法將它們加入至 [parameters](./parameters-collection-ado.md) 集合。 這可讓您設定和傳回參數值，而不需要呼叫**Parameters**集合上的[Refresh](./refresh-method-ado.md)方法，以從提供者取出參數資訊，這是可能需要大量資源的作業。  
  
 **參數**物件對腳本是不安全的。  
  
 本節包含下列主題。  
  
-   [Parameter 物件屬性、方法和事件](./parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的命令物件 ](./command-object-ado.md)   
 [ (ADO) 的 CreateParameter 方法 ](./createparameter-method-ado.md)   
 [ (ADO) 的參數集合 ](./parameters-collection-ado.md)   
 [Properties 集合 (ADO)](./properties-collection-ado.md)