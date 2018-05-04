---
title: CommandStream 屬性 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7bfaf04f8be778aac51d08c93eb9e9b7290b8df
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="commandstream-property-ado"></a>CommandStream 屬性 (ADO)
表示用來做為輸入資料流[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回用來做為輸入資料流**命令**物件。 這個資料流的格式是提供者特有的。請參閱您的提供者文件，如需詳細資訊。 這個屬性是類似於[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性，用來指定的輸入字串**命令**。  
  
## <a name="remarks"></a>備註  
 **CommandStream**和**CommandText**互為獨佔模式。 當使用者設定**CommandStream**屬性， **CommandText**屬性會設定為空字串 ("")。 如果使用者設定**CommandText**屬性， **CommandStream**屬性將設定為**Nothing**。  
  
 行為**Command.Parameters.Refresh**和**Command.Prepare**提供者所定義的方法。 資料流中的參數的值不可以重新整理。  
  
 輸入資料流不適用於其他 ADO 物件來源會傳回**命令**。 例如，如果[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)的[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)設**命令**具有做為輸入，資料流的物件**Recordset.Source**會繼續傳回**CommandText**屬性，其中包含空字串 ("")，而不是資料流內容的**CommandStream**屬性。  
  
 使用命令資料流時 (所指定**CommandStream**)，唯一有效[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性**adCmdText**和**adCmdUnknown**。 任何其他值會導致錯誤。  
  
## <a name="applies-to"></a>適用於  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CommandText 屬性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [方言屬性](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
