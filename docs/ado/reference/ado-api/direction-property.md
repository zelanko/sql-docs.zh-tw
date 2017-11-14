---
title: "方向屬性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::Direction
helpviewer_keywords:
- Direction property
ms.assetid: d5732578-3434-4dcd-a9f7-db1abd1b3b94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a81c60a4505e1c5e420583c474109d0d08f4fb6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="direction-property"></a>方向屬性
指出是否[參數](../../../ado/reference/ado-api/parameter-object.md)代表輸入的參數、 輸出參數、 輸入和輸出參數，或如果參數是預存程序的傳回值。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)值。  
  
## <a name="remarks"></a>備註  
 使用**方向**屬性來指定從程序或方式傳遞的參數。 **方向**屬性是讀取/寫入; 這可讓您搭配不傳回這項資訊的提供者，或是當您不想讓額外的提供者呼叫以擷取參數資訊的 ADO 設定這項資訊。  
  
 並非所有提供者可以判斷其預存程序中的參數方向。 在這些情況下，您必須設定**方向**屬性，然後再執行查詢。  
  
## <a name="applies-to"></a>適用於  
 [參數物件](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)

