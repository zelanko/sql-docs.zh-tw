---
title: CommandType 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandType
helpviewer_keywords:
- CommandType property [ADO]
ms.assetid: ca44809c-8647-48b6-a7fb-0be70a02f53e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6612a90b94f10bdd08441d7814a7137121659045
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63316002"
---
# <a name="commandtype-property-ado"></a>CommandType 屬性 (ADO)
表示的型別[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回一或多個[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值。  
  
> [!NOTE]
>  請勿使用**CommandTypeEnum**的值**adCmdFile**或是**adCmdTableDirect**具有**CommandType**。 這些值只可用來當做選項搭配[開放](../../../ado/reference/ado-api/open-method-ado-recordset.md)並[Requery](../../../ado/reference/ado-api/requery-method.md)方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="remarks"></a>備註  
 使用**CommandType**屬性，以最佳化的評估結果[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性。  
  
 如果**CommandType**屬性值設為預設值為**adCmdUnknown**，您可能會感覺到的效能，因為 ADO 必須進行呼叫提供者，以判斷**CommandText**屬性是 SQL 陳述式、 預存程序中或資料表名稱。 如果您知道您正在使用的命令類型，則設定**CommandType**屬性會指示 ADO，直接移至相關的程式碼。 如果**CommandType**屬性不符合命令中的型別**CommandText**屬性，您呼叫時發生錯誤[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法。  
  
## <a name="applies-to"></a>適用於  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
