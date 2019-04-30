---
title: CommandStream 屬性 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b1048e8d243bd19d86d60c3c4f92e4e4b9d137a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267283"
---
# <a name="commandstream-property-ado"></a>CommandStream 屬性 (ADO)
表示用做為輸入的資料流[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回做為輸入使用的資料流**命令**物件。 這個資料流的格式是特定提供者;請參閱您的提供者文件，如需詳細資訊。 這個屬性是類似[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性，用來指定之型別的字串**命令**。  
  
## <a name="remarks"></a>備註  
 **CommandStream**並**CommandText**互斥。 當使用者設定**CommandStream**屬性， **CommandText**屬性會設定為空字串 ("")。 如果使用者設定**CommandText**屬性， **CommandStream**屬性會設定為**Nothing**。  
  
 行為**Command.Parameters.Refresh**並**Command.Prepare**提供者所定義的方法。 可以重新整理的資料流中的參數值。  
  
 輸入資料流不適用於其他 ADO 物件傳回的來源**命令**。 比方說，如果[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)的[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)設定為**命令**物件，具有做為輸入，串流**Recordset.Source**會繼續傳回**CommandText**屬性，其中包含空字串 ("")，而不是資料流內容**CommandStream**屬性。  
  
 使用命令資料流時 (所指定**CommandStream**)，唯一有效[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性**adCmdText**並**adCmdUnknown**。 任何其他值會導致錯誤。  
  
## <a name="applies-to"></a>適用於  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CommandText 屬性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Dialect 屬性](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
