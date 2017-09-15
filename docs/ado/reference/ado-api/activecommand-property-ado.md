---
title: "ActiveCommand 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4b1580dbedaa9c7667cd7b320817fdaea6ad48d7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="activecommand-property-ado"></a>ActiveCommand 屬性 (ADO)
指出[命令](../../../ado/reference/ado-api/command-object-ado.md)建立相關聯的物件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回**Variant**包含**命令**物件。 預設值為 null 物件的參考。  
  
## <a name="remarks"></a>備註  
 **ActiveCommand**屬性是唯讀的。  
  
 如果**命令**物件不用來建立目前**資料錄集**，則**Null**會傳回物件的參考。  
  
 使用這個屬性來尋找相關聯**命令**物件時，您可以只產生**資料錄集**物件。  
  
## <a name="applies-to"></a>適用於  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActiveCommand 屬性範例 (VB)](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [ActiveCommand 屬性範例 (JScript)](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [ActiveCommand 屬性範例 （VC + +）](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [命令物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)

