---
title: "Microsoft 資料成形 OLE DB （ADO 服務提供者） 的服務 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3510664e97b64c36b7c1c7b42ca475194b6d01e2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Microsoft 資料成形服務 OLE DB 概觀
> [!IMPORTANT]
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，應用程式應該使用 XML。

 Microsoft Data Shaping Service 的 OLE DB 服務提供者支援階層式建構 （形狀）[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)從資料提供者的物件。

## <a name="provider-keyword"></a>提供者關鍵字
 若要叫用 Data Shaping Service 的 OLE DB 時，指定下列關鍵字和值的連接字串中。

```
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>動態屬性
 叫用此服務提供者時，已加入下列的動態屬性[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。

|動態屬性名稱|Description|
|---------------------------|-----------------|
|**唯一的重繪名稱**|指出是否**資料錄集**具有重複值的物件及其**重繪名稱**不允許屬性。 如果此動態屬性是**True**和新**資料錄集**建立與使用者指定的重繪同名的現有**資料錄集**，然後新**資料錄集**修改物件的重繪名稱成為唯一。 如果這個屬性是**False**和新**資料錄集**建立與使用者指定的重繪同名的現有**資料錄集**，這兩個**資料錄集**物件會具有相同的重繪名稱。 因此，兩者皆非**資料錄集**可重繪，只要存在兩個資料錄集。<br /><br /> 屬性的預設值是**False**。|
|**資料提供者**|表示將會提供圖形化的資料列的提供者的名稱。 如果提供者不會使用提供的資料列，這個值可以無。|

 您也可以指定其名稱為連接字串中的關鍵字，以設定可寫入的動態屬性。 例如，在 Microsoft Visual Basic 中，設定**資料提供者**"MSDASQL 」 藉由指定動態屬性：

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 您也可以設定或擷取動態屬性，藉由指定其名稱為的索引[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)屬性。 例如，下列程式碼範例取得並列印的目前值**資料提供者**動態屬性，然後設定新的值，如果 cn。DataProvider 已設定為"MSDataShape 」 (直接或間接透過連接字串) 和未開啟連線：

```
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  動態屬性，**資料提供者**，可以設定只有在未開啟**連接**物件。 一旦開啟連接時，**資料提供者**屬性會變成唯讀。

 如需資料成形的詳細資訊，請參閱[資料成形](../../../ado/guide/data/data-shaping-overview.md)。

## <a name="see-also"></a>另請參閱
 [附錄 a： 提供者](../../../ado/guide/appendixes/appendix-a-providers.md)

