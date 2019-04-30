---
title: Direction 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Direction
helpviewer_keywords:
- Direction property
ms.assetid: d5732578-3434-4dcd-a9f7-db1abd1b3b94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df2f7cc5eadce7d4f8f61674f4915ec3b1561e02
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63180967"
---
# <a name="direction-property"></a>Direction 屬性
指出是否[參數](../../../ado/reference/ado-api/parameter-object.md)代表輸入的參數、 輸出參數、 輸入和一個 output 參數，或如果參數是預存程序的傳回值。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)值。  
  
## <a name="remarks"></a>備註  
 使用**方向**屬性來指定參數如何傳遞至或從程序。 **方向**屬性是讀取/寫入，這可讓您搭配不傳回這項資訊的提供者，或當您不想要進行額外呼叫提供者擷取參數資訊的 ADO 設定這項資訊。  
  
 並非所有提供者可以判斷其預存程序中的參數方向。 在這些情況下，您必須設定**方向**屬性在執行查詢。  
  
## <a name="applies-to"></a>適用於  
 [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
