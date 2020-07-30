---
title: Refresh 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 0688fc8b45f444ca8c711f3229623484fa2139a8
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242578"
---
# <a name="refresh-method-ado"></a>Refresh 方法 (ADO)
更新集合中的物件，以反映提供者所提供的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>備註  
 **Refresh**方法會根據您呼叫它的集合，來完成不同的工作。  
  
### <a name="parameters"></a>參數  
 在[command](../../../ado/reference/ado-api/command-object-ado.md)物件的[Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合上使用**Refresh**方法，會針對**command**物件中指定的預存程式或參數化查詢，抓取提供者端參數資訊。 對於不支援預存程序呼叫或參數化查詢的提供者，集合將會是空的。  
  
 您應該將**Command**物件的[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性設為有效的[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件、 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性為有效的命令，並將[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性設定為**adCmdStoredProc** ，再呼叫**Refresh**方法。  
  
 如果您在呼叫**Refresh**方法之前存取**PARAMETERS**集合，ADO 會自動呼叫方法並為您填入集合。  
  
> [!NOTE]
>  如果您使用**Refresh**方法從提供者取得參數資訊，並傳回一或多個可變長度的資料類型[參數](../../../ado/reference/ado-api/parameter-object.md)物件，ADO 可能會根據其最大可能大小來配置參數的記憶體，這會在執行期間造成錯誤。 您應該先明確設定這些參數的[Size](../../../ado/reference/ado-api/size-property-ado-parameter.md)屬性，再呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法來避免發生錯誤。  
  
### <a name="fields"></a>欄位  
 在[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合上使用**Refresh**方法不會顯示任何效果。 若要從基礎資料庫結構中抓取變更，您必須使用[Requery](../../../ado/reference/ado-api/requery-method.md)方法，或者，如果[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件不支援書簽，則是[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。  
  
### <a name="properties"></a>屬性  
 在某些物件的**屬性**集合上使用**Refresh**方法，會在集合中填入提供者所公開的動態屬性。 除了 ADO 支援的內建屬性以外，這些屬性會提供提供者特定功能的相關資訊。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [軸集合](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)  
        [Columns 集合](../../../ado/reference/adox-api/columns-collection-adox.md)  
        [CubeDefs 集合](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)  
        [維度集合](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)  
        [錯誤集合](../../../ado/reference/ado-api/errors-collection-ado.md)  
        [Fields 集合](../../../ado/reference/ado-api/fields-collection-ado.md)  
        [群組集合](../../../ado/reference/adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [階層集合](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)  
        [索引集合](../../../ado/reference/adox-api/indexes-collection-adox.md)  
        [金鑰集合](../../../ado/reference/adox-api/keys-collection-adox.md)  
        [層級集合](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)  
        [Members 集合](../../../ado/reference/ado-md-api/members-collection-ado-md.md)  
        [Parameters 集合](../../../ado/reference/ado-api/parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [位置集合](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)  
        [程式集合](../../../ado/reference/adox-api/procedures-collection-adox.md)  
        [屬性集合](../../../ado/reference/ado-api/properties-collection-ado.md)  
        [資料表集合](../../../ado/reference/adox-api/tables-collection-adox.md)  
        [Users 集合](../../../ado/reference/adox-api/users-collection-adox.md)  
        [Views 集合](../../../ado/reference/adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [Refresh 方法範例（VB）](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Refresh 方法範例（VC + +）](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Count 屬性（ADO）](../../../ado/reference/ado-api/count-property-ado.md)   
 [Refresh 方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
