---
title: Microsoft 資料成形 OLE DB （ADO 服務提供者） 的服務 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46f48aa117c18bcc7af28cdf7c676cf195b553f6
ms.sourcegitcommit: 96b2355d54dfad259826e88bdff91cc9344e16f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2018
ms.locfileid: "51350062"
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Microsoft 資料成形 Service for OLE DB 概觀
> [!IMPORTANT]
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，應用程式應該使用 XML。

 Microsoft Data Shaping Service 的 OLE DB 服務提供者支援階層式建構 （形狀）[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)從資料提供者的物件。

## <a name="provider-keyword"></a>提供者關鍵字
 要叫用 OLE DB Data Shaping Service，請連接字串中指定下列關鍵字和值。

```vb
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>動態屬性
 叫用此服務提供者時，加入下列的動態屬性[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件。

|動態屬性名稱|描述|
|---------------------------|-----------------|
|**唯一的重繪名稱**|指出是否**資料錄集**具有重複值的物件及其**調整形狀名稱**不允許屬性。 如果此動態屬性 **，則為 True**和新**資料錄集**建立與使用者指定的重繪同名的現有**資料錄集**，則新**資料錄集**修改物件的重繪名稱使其成為唯一。 如果這個屬性是**假**和新**資料錄集**建立具有相同的使用者指定的重繪名稱與現有**資料錄集**，這兩個**資料錄集**物件會具有相同的重繪名稱。 因此，兩者皆非**資料錄集**可重繪，只要這兩個資料錄集存在。<br /><br /> 屬性的預設值是**False**。|
|**資料提供者**|表示將會提供圖形化的資料列提供者的名稱。 這個值可以是 NONE，如果提供者不會用來提供資料列。|

 您也可以藉由指定其名稱為關鍵字的連接字串中設定可寫入的動態屬性。 例如，在 Microsoft Visual Basic 中，設定**資料提供者**動態屬性 」 MSDASQL 」 藉由指定：

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 您也可以設定，或藉由指定其名稱為索引中擷取動態屬性[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)屬性。 例如，下列程式碼範例會取得並列印目前的值**資料提供者**動態屬性，然後設定新的值，如果 cn。DataProvider 已設為"MSDataShape 」 (直接或間接透過連接字串) 和未開啟連接：

```vb
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  動態屬性**資料提供者**，可以設定只有在未開啟**連線**物件。 開啟連接時，一旦**資料提供者**屬性會變成唯讀。

 如需資料成形的詳細資訊，請參閱[資料成形](../../../ado/guide/data/data-shaping-overview.md)。

## <a name="see-also"></a>另請參閱
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
