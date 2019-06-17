---
title: Size 屬性 (ADO Parameter) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: caad25759038fde0107fa7602394de2a8a01e38c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711492"
---
# <a name="size-property-ado-parameter"></a>Size 屬性 (ADO 參數)
表示的最大的大小，以位元組或字元，[參數](../../../ado/reference/ado-api/parameter-object.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**值，指出在的中值的字元或位元組的大小上限**參數**物件。  
  
## <a name="remarks"></a>備註  
 使用**大小**屬性來判斷的值寫入的大小上限，或從讀取[值](../../../ado/reference/ado-api/value-property-ado.md)屬性**參數**物件。  
  
 如果您指定的可變長度資料類型**參數**物件 (例如，任何**字串**類型，例如**adVarChar**)，您必須設定物件的**大小**屬性，才能將它附加[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合; 否則會發生錯誤。  
  
 如果您已經有附加**參數**物件**參數**集合[命令](../../../ado/reference/ado-api/command-object-ado.md)物件，而且您變更其類型為可變長度資料類型，您必須設定**參數**物件的**大小**屬性，才能執行**命令**物件; 否則會發生錯誤。  
  
 如果您使用[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)從提供者，並取得參數資訊的方法會傳回一或多個可變長度資料類型**參數**物件時，ADO 可能配置的記憶體為基礎的參數在其最大潛在大小，這可能會在執行期間造成錯誤。 若要避免錯誤，您應該明確設定**大小**這些參數執行命令之前的屬性。  
  
 **大小**屬性是讀取/寫入。  
  
## <a name="applies-to"></a>適用於  
 [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Size 屬性 (ADO Stream)](../../../ado/reference/ado-api/size-property-ado-stream.md)
