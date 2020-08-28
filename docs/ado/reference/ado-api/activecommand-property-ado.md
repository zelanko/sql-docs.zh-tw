---
description: ActiveCommand 屬性 (ADO)
title: " (ADO) 的 ActiveCommand 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: df737543e8cc09735c7da413b89406b6f2385079
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977150"
---
# <a name="activecommand-property-ado"></a>ActiveCommand 屬性 (ADO)
指出建立相關聯[記錄集](./recordset-object-ado.md)物件的[命令](./command-object-ado.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回包含**Command**物件的**Variant** 。 預設值為 null 物件參考。  
  
## <a name="remarks"></a>備註  
 **ActiveCommand**屬性是唯讀的。  
  
 如果未使用 **命令** 物件來建立目前的 **記錄集**，則會傳回 **Null** 物件參考。  
  
 當您只獲得產生的**記錄集**物件時，請使用這個屬性來尋找相關聯的**命令**物件。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 ActiveCommand 屬性範例 ](./activecommand-property-example-vb.md)   
 [ActiveCommand 屬性範例 (JScript) ](./activecommand-property-example-jscript.md)   
 [ActiveCommand 屬性範例 (VC + +) ](./activecommand-property-example-vc.md)   
 [Command 物件 (ADO)](./command-object-ado.md)