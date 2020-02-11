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
ms.openlocfilehash: 6135650d3b5cb015fad21d1eac7b350827965ca1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933071"
---
# <a name="direction-property"></a>Direction 屬性
指出[參數](../../../ado/reference/ado-api/parameter-object.md)是否代表輸入參數、輸出參數、輸入和輸出參數，或參數是否為預存程式的傳回值。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)值。  
  
## <a name="remarks"></a>備註  
 使用**Direction**屬性可指定如何在程式中傳遞參數。 **Direction**屬性為讀取/寫入;這可讓您使用不會傳回此資訊的提供者，或在您不想要讓 ADO 對提供者進行額外呼叫來取得參數資訊時，設定此資訊。  
  
 並非所有提供者都可以判斷其預存程式中的參數方向。 在這些情況下，您必須在執行查詢之前設定**Direction**屬性。  
  
## <a name="applies-to"></a>套用至  
 [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（VB）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（JScript）](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
