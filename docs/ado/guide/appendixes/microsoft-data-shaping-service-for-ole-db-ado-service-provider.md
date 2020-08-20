---
description: '適用于 OLE DB (ADO 服務提供者的 Microsoft 資料成形服務) '
title: 適用于 OLE DB (ADO 服務提供者的 Microsoft 資料成形服務) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
author: rothja
ms.author: jroth
ms.openlocfilehash: 3c61e40220b99bd68c92e2651d58ea13ee10be29
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454100"
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>適用于 OLE DB 的 Microsoft 資料成形服務總覽
> [!IMPORTANT]
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，應用程式應該使用 XML。

 適用于 OLE DB 服務提供者的 Microsoft 資料成形服務可支援從資料提供者塑造階層式 (圖形) [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件。

## <a name="provider-keyword"></a>Provider 關鍵字
 若要叫用 OLE DB 的資料成形服務，請在連接字串中指定下列關鍵字和值。

```vb
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>動態屬性
 叫用此服務提供者時，會將下列動態屬性加入至[Connection](../../../ado/reference/ado-api/connection-object-ado.md)物件的[properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合中。

|動態屬性名稱|描述|
|---------------------------|-----------------|
|**獨特的改變名稱**|指出是否允許具有重複之重設其**名稱**屬性值的**記錄集**物件。 如果這個動態屬性為 **True** ，且建立新的 **記錄集** 時，具有與現有 **記錄集**相同的使用者指定重設名稱，則會修改新的 **記錄集** 物件的重新調整名稱，使其成為唯一的。 如果這個屬性為 **False** ，且建立的新 **記錄集** 具有與現有 **記錄集**相同的使用者指定重設名稱，則這兩個 **記錄集** 物件將會有相同的改變名稱。 因此，只要兩個記錄集都存在，就不會改變任何 **記錄集** 。<br /><br /> 屬性的預設值為 **False**。|
|**Data Provider**|指出將提供要塑造之資料列的提供者名稱。 如果提供者不會用來提供資料列，這個值可以是 NONE。|

 您也可以藉由在連接字串中將其名稱指定為關鍵字，來設定可寫入動態屬性。 例如，在 Microsoft Visual Basic 中，藉由指定下列各項，將 **Data Provider** 動態屬性設定為 "MSDASQL"：

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 您也可以藉由將動態屬性的名稱指定為 [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) 屬性的索引，來設定或取出動態屬性。 例如，下列程式碼範例會取得並列印 **Data Provider** 動態屬性的目前值，然後設定新值（如果 cn）。DataProvider 已設定為 "MSDataShape" (直接或間接透過連接字串) ，而且尚未開啟連接：

```vb
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  只有未開啟的**連接**物件可以設定動態屬性（ **Data Provider**）。 一旦開啟連接， **Data Provider** 屬性就會變成隻讀。

 如需資料成形的詳細資訊，請參閱 [資料成形](../../../ado/guide/data/data-shaping-overview.md)。

## <a name="see-also"></a>另請參閱
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
