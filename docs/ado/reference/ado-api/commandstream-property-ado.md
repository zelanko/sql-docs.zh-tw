---
title: CommandStream 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23ec65380bfea16d38f02cab0a070ab69f85d525
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919740"
---
# <a name="commandstream-property-ado"></a>CommandStream 屬性 (ADO)
指出當做[命令](../../../ado/reference/ado-api/command-object-ado.md)物件之輸入使用的資料流程。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回用來做為**命令**物件輸入的資料流程。 此資料流程的格式是提供者特定的;如需詳細資訊，請參閱提供者的檔。 這個屬性與[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性相似，後者是用來指定**命令**輸入的字串。  
  
## <a name="remarks"></a>備註  
 **CommandStream**和**CommandText**相互排斥。 當使用者設定**CommandStream**屬性時， **CommandText**屬性會設定為空字串（""）。 如果使用者設定**CommandText**屬性， **CommandStream**屬性將會設定為 [**無**]。  
  
 命令的行為 **。 Parameters. Refresh**和**command。 Prepare**方法是由提供者定義。 資料流程中的參數值不能重新整理。  
  
 輸入資料流程無法供傳回**命令**來源的其他 ADO 物件使用。 例如，如果[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)設定為具有資料流程做為輸入的**命令**物件，則**記錄集。來源**會繼續傳回**CommandText**屬性，其中包含空字串（""），而不是**CommandStream**屬性的資料流程內容。  
  
 當使用命令資料流程（如**CommandStream**所指定）時， [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性唯一有效的[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值為**adCmdText**和**adCmdUnknown**。 其他任何值會造成錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CommandText 屬性（ADO）](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [方言屬性](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
