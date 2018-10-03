---
title: Refresh 方法 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcba9515535e32557470b75267a0e99976a18595
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681618"
---
# <a name="refresh-method-ado"></a>Refresh 方法 (ADO)
更新物件來反映，從可用的物件的集合以及特定給提供者。  
  
## <a name="syntax"></a>語法  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>備註  
 **重新整理**方法會完成不同的工作，視您呼叫它的集合。  
  
### <a name="parameters"></a>參數  
 使用**重新整理**方法[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合[命令](../../../ado/reference/ado-api/command-object-ado.md)物件會擷取預存程序的提供者端參數資訊或中指定的參數化的查詢**命令**物件。 集合會是空的不支援預存程序呼叫或參數化的查詢的提供者。  
  
 您應該設定[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性**命令**設為有效的物件[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性以有效的命令，而[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性設**adCmdStoredProc**再呼叫**重新整理**方法。  
  
 如果您存取**參數**集合，然後再呼叫**重新整理**方法，ADO 會自動呼叫的方法，並填入您的集合。  
  
> [!NOTE]
>  如果您使用**重新整理**從提供者，並取得參數資訊的方法會傳回一或多個可變長度資料類型[參數](../../../ado/reference/ado-api/parameter-object.md)物件時，ADO 可能配置的記憶體為基礎的參數其最大的潛在大小，這會導致在執行期間發生錯誤。 您應該明確設定[大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)屬性，這些參數，然後再呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法，以避免發生錯誤。  
  
### <a name="fields"></a>欄位  
 使用**重新整理**方法[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合沒有任何可見的作用。 若要擷取基礎資料庫結構中的變更，您必須使用[Requery](../../../ado/reference/ado-api/requery-method.md)方法或是如果[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件不支援書籤， [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。  
  
### <a name="properties"></a>屬性  
 使用**重新整理**方法**屬性**某些物件的集合，以填入集合的提供者會公開之動態屬性。 這些屬性會提供給提供者，除了內建屬性 ADO 支援特定功能的相關資訊。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Axes 集合](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[資料行集合](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs 集合](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Dimensions 集合](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[錯誤集合](../../../ado/reference/ado-api/errors-collection-ado.md)|[Fields 集合](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[群組集合](../../../ado/reference/adox-api/groups-collection-adox.md)|[Hierarchies 集合](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Indexes 集合](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Keys 集合](../../../ado/reference/adox-api/keys-collection-adox.md)|[Levels 集合](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Members 集合](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Parameters 集合](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Positions 集合](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Procedures 集合](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[屬性集合](../../../ado/reference/ado-api/properties-collection-ado.md)|[Tables 集合](../../../ado/reference/adox-api/tables-collection-adox.md)|[使用者集合](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Views 集合](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>另請參閱  
 [Refresh 方法範例 (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Refresh 方法範例 （VC + +）](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Count 屬性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Refresh 方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
