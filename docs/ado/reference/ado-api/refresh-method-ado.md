---
description: Refresh 方法 (ADO)
title: " (ADO) 的 Refresh 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords:
- Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
author: rothja
ms.author: jroth
ms.openlocfilehash: 66324860f931a919cccc36d3de9464d2ad2e48d0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989609"
---
# <a name="refresh-method-ado"></a>Refresh 方法 (ADO)
更新集合中的物件，以反映可供提供者使用的物件，以及特定的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>備註  
 重新 **整理方法會** 根據您從中呼叫的集合來完成不同的工作。  
  
### <a name="parameters"></a>參數  
 在[command](./command-object-ado.md)物件的[Parameters](./parameters-collection-ado.md)集合上使用**Refresh**方法，會抓取**命令**物件中所指定預存程式或參數化查詢的提供者端參數資訊。 對於不支援預存程序呼叫或參數化查詢的提供者而言，集合將會是空的。  
  
 您應該將**命令**物件的[ActiveConnection](./activeconnection-property-ado.md)屬性設定為有效的[連接](./connection-object-ado.md)物件、 [CommandText](./commandtext-property-ado.md)屬性設為有效的命令，並將[CommandType](./commandtype-property-ado.md)屬性設定為在呼叫**Refresh**方法之前**adCmdStoredProc** 。  
  
 如果您在呼叫**Refresh**方法之前存取了**Parameters**集合，則 ADO 會自動呼叫方法並為您填入集合。  
  
> [!NOTE]
>  如果您使用 **Refresh** 方法從提供者取得參數資訊，而且它會傳回一或多個可變長度的資料類型 [參數](./parameter-object.md) 物件，則 ADO 可能會根據其最大可能大小來配置參數的記憶體，這會在執行期間造成錯誤。 您應該先明確設定這些參數的 [Size](./size-property-ado-parameter.md) 屬性，然後再呼叫 [Execute](./execute-method-ado-command.md) 方法，以避免發生錯誤。  
  
### <a name="fields"></a>欄位  
 在[Fields](./fields-collection-ado.md)集合上使用**Refresh**方法沒有任何可見效果。 若要從基礎資料庫結構取出變更，您必須使用 [Requery](./requery-method.md) 方法，或者，如果 [記錄集](./recordset-object-ado.md) 物件不支援書簽，則必須使用 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 方法。  
  
### <a name="properties"></a>屬性  
 在某些物件的**屬性**集合上使用**Refresh**方法，會在集合中填入提供者公開的動態屬性。 除了 ADO 支援的內建屬性之外，這些屬性也提供提供者特定功能的相關資訊。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [軸集合](../ado-md-api/axes-collection-ado-md.md)  
        [Columns 集合](../adox-api/columns-collection-adox.md)  
        [CubeDefs 集合](../ado-md-api/cubedefs-collection-ado-md.md)  
        [維度集合](../ado-md-api/dimensions-collection-ado-md.md)  
        [錯誤集合](./errors-collection-ado.md)  
        [Fields 集合](./fields-collection-ado.md)  
        [群組集合](../adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [階層集合](../ado-md-api/hierarchies-collection-ado-md.md)  
        [索引集合](../adox-api/indexes-collection-adox.md)  
        [金鑰集合](../adox-api/keys-collection-adox.md)  
        [層級集合](../ado-md-api/levels-collection-ado-md.md)  
        [成員集合](../ado-md-api/members-collection-ado-md.md)  
        [Parameters 集合](./parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [位置集合](../ado-md-api/positions-collection-ado-md.md)  
        [程式集合](../adox-api/procedures-collection-adox.md)  
        [屬性集合](./properties-collection-ado.md)  
        [資料表集合](../adox-api/tables-collection-adox.md)  
        [使用者集合](../adox-api/users-collection-adox.md)  
        [Views 集合](../adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [Refresh 方法範例 (VB) ](./refresh-method-example-vb.md)   
 [ (VC + +) 的 Refresh 方法範例 ](./refresh-method-example-vc.md)   
 [Count 屬性 (ADO) ](./count-property-ado.md)   
 [Refresh 方法 (RDS)](../rds-api/refresh-method-rds.md)