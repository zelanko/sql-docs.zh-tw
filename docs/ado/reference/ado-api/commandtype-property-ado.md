---
title: "CommandType 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Command15::CommandType
helpviewer_keywords: CommandType property [ADO]
ms.assetid: ca44809c-8647-48b6-a7fb-0be70a02f53e
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7d838b150f678fc0ee720a91d2a1de3311a433e7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="commandtype-property-ado"></a>CommandType 屬性 (ADO)
表示的類型[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回一或多個[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值。  
  
> [!NOTE]
>  請勿使用**CommandTypeEnum**值**adCmdFile**或**adCmdTableDirect**與**CommandType**。 這些值只用於做為選項與[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)和[Requery](../../../ado/reference/ado-api/requery-method.md)方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="remarks"></a>備註  
 使用**CommandType**屬性，以最佳化評估[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性。  
  
 如果**CommandType**屬性值設定為預設值為**adCmdUnknown**，您可能會感覺到的效能降低，因為 ADO 必須進行的呼叫提供者，以判斷是否**CommandText**屬性是 SQL 陳述式、 預存程序或資料表名稱。 如果您知道您使用何種命令，設定**CommandType**屬性會指示 ADO 可直接前往相關的程式碼。 如果**CommandType**屬性不相符的類型中的命令**CommandText**屬性，就會發生錯誤時呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法。  
  
## <a name="applies-to"></a>適用於  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>請參閱  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
