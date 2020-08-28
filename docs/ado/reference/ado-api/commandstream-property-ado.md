---
description: CommandStream 屬性 (ADO)
title: " (ADO) 的 CommandStream 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 463468f8e39d1187a36ac6fa1279e8a2aeb3a73b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975199"
---
# <a name="commandstream-property-ado"></a>CommandStream 屬性 (ADO)
表示用來當做 [命令](./command-object-ado.md) 物件輸入的資料流程。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回用來當做 **命令** 物件之輸入的資料流程。 此資料流程的格式為提供者特定;請參閱提供者的檔以取得詳細資料。 這個屬性與 [CommandText](./commandtext-property-ado.md) 屬性類似，後者是用來指定 **命令**輸入的字串。  
  
## <a name="remarks"></a>備註  
 **CommandStream** 和 **CommandText** 互相排斥。 當使用者設定 **CommandStream** 屬性時， **CommandText** 屬性將會設為空字串 ( "" ) 。 如果使用者設定 **CommandText** 屬性， **CommandStream** 屬性將會設定為 **Nothing**。  
  
 命令的行為。 **Parameters. Refresh** 和 **command. Prepare** 方法是由提供者定義。 資料流程中的參數值不能重新整理。  
  
 傳回 **命令**來源的其他 ADO 物件無法使用輸入資料流程。 例如，如果[記錄集](./recordset-object-ado.md)的[來源](./source-property-ado-recordset.md)設定為具有資料流程作為其輸入的**命令**物件，則**會繼續傳回** **CommandText**屬性，此屬性包含 ( "" ) 的空字串，而不是**CommandStream**屬性的資料流程內容。  
  
 當您使用**CommandStream**) 所指定的命令資料流程 (時， [CommandType](./commandtype-property-ado.md)屬性唯一有效的[CommandTypeEnum](./commandtypeenum.md)值是**adCmdText**和**adCmdUnknown**。 其他任何值會造成錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Command 物件 (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 CommandText 屬性 ](./commandtext-property-ado.md)   
 [方言屬性](./dialect-property.md)   
 [CommandTypeEnum](./commandtypeenum.md)