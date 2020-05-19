---
title: ActiveCommand 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
author: rothja
ms.author: jroth
ms.openlocfilehash: b89876366c80d20bde110da9e9d86414873e86bc
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747480"
---
# <a name="activecommand-property-ado"></a>ActiveCommand 屬性 (ADO)
表示建立相關聯[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回包含**命令**物件的**Variant** 。 預設值為 null 物件參考。  
  
## <a name="remarks"></a>備註  
 **ActiveCommand**屬性是唯讀的。  
  
 如果**命令**物件不是用來建立目前的**記錄集**，則會傳回**Null**物件參考。  
  
 當您只提供產生的**記錄集**物件時，請使用這個屬性來尋找相關聯的**命令**物件。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActiveCommand 屬性範例（VB）](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [ActiveCommand 屬性範例（JScript）](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [ActiveCommand 屬性範例（VC + +）](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
