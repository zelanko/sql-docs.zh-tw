---
description: CommandType 屬性 (ADO)
title: " (ADO) 的 CommandType 屬性 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 435e2c0562abcccbb6ec6e139491af280e976cfd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450810"
---
# <a name="commandtype-property-ado"></a>CommandType 屬性 (ADO)
表示 [Command](../../../ado/reference/ado-api/command-object-ado.md) 物件的型別。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回一或多個 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 值。  
  
> [!NOTE]
>  請勿搭配**CommandType**使用**adCmdFile**或**adCmdTableDirect**的**CommandTypeEnum**值。 這些值只能當做選項來使用[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)和重新[查詢](../../../ado/reference/ado-api/requery-method.md)方法。  
  
## <a name="remarks"></a>備註  
 使用 **CommandType** 屬性可優化 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 屬性的評估。  
  
 如果 **CommandType** 屬性值設定為預設值 **adCmdUnknown**，您可能會遇到效能降低的情況，因為 ADO 必須對提供者進行呼叫，以判斷 **CommandText** 屬性是 SQL 語句、預存程式或資料表名稱。 如果您知道所使用的命令類型，設定 **CommandType** 屬性會指示 ADO 直接前往相關的程式碼。 如果 **CommandType** 屬性不符合 **CommandText** 屬性中的命令類型，當您呼叫 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 方法時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (VB) ](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (VC + +) ](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (JScript) ](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
