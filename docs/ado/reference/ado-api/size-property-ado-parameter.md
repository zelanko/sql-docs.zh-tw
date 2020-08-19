---
description: Size 屬性 (ADO 參數)
title: Size 屬性 (ADO 參數) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Size
helpviewer_keywords:
- Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 78a22e22f5bf65c211a18bd68767537af164b452
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442150"
---
# <a name="size-property-ado-parameter"></a>Size 屬性 (ADO 參數)
指出 [參數](../../../ado/reference/ado-api/parameter-object.md) 物件的大小上限（以位元組或字元為單位）。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **Long** 值，指出 **參數** 物件中值的大小上限（以位元組為單位）或字元數上限。  
  
## <a name="remarks"></a>備註  
 您可以使用 [**大小**] 屬性來決定在**參數**物件的[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性中寫入或讀取之值的大小上限。  
  
 如果您指定 **參數** 物件的可變長度資料類型 (例如，任何 **字串** 類型，例如 **adVarChar**) ，您必須先設定物件的 **Size** 屬性，然後再將它附加至 [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) 集合;否則，就會發生錯誤。  
  
 如果您已經將**參數**物件附加至[Command](../../../ado/reference/ado-api/command-object-ado.md)物件的**Parameters**集合，並將其類型變更為可變長度的資料類型，則必須先設定**參數**物件的**Size**屬性，才能執行**Command**物件。否則，就會發生錯誤。  
  
 如果您使用 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 方法從提供者取得參數資訊，而且它會傳回一或多個可變長度的資料類型 **參數** 物件，則 ADO 可能會根據其最大可能大小來配置參數的記憶體，這可能會在執行期間造成錯誤。 若要避免發生錯誤，您應該先明確設定這些參數的 **Size** 屬性，然後再執行命令。  
  
 **Size**屬性為 read/write。  
  
## <a name="applies-to"></a>套用至  
 [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (VB) ](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (VC + +) ](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (JScript) ](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Size 屬性 (ADO Stream)](../../../ado/reference/ado-api/size-property-ado-stream.md)
