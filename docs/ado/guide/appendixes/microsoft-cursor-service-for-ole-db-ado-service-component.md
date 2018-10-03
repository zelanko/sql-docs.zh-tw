---
title: OLE DB （ADO 服務元件） 的 Microsoft 資料指標服務 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c859de289a9f93a23702c63bd50269bb0881b34
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47714986"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>OLE DB 概觀的 Microsoft 資料指標服務
OLE DB 的 Microsoft 資料指標服務來補充資料提供者的資料指標支援函式。 如此一來，使用者察覺到相當一致的功能，從所有資料提供者。

 資料指標服務提供動態屬性，並增強特定方法的行為。 例如，[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)動態屬性可讓您建立暫存的索引，以利於進行某些作業，例如[尋找](../../../ado/reference/ado-api/find-method-ado.md)方法。

 資料指標服務可支援在所有情況下的批次更新。 資料提供者只可以提供效能較差的資料指標，例如靜態資料指標時，它也會模擬功能更強大的資料指標類型，例如動態資料指標。

## <a name="keyword"></a>關鍵字
 若要叫用此服務元件，請設定[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件的[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設**adUseClient**。

```
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>動態屬性
 叫用的 OLE DB 資料指標服務時，加入下列的動態屬性**Recordset**物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。 完整清單**連接**並**Recordset**物件的動態屬性會列在[ADO 動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)。 相關聯的 OLE DB 屬性名稱，在適當的地方包含括號括住的 ADO 屬性名稱之後。

 有些動態屬性的變更不會對基礎資料來源顯示的在叫用資料指標服務之後。 例如，設定*命令逾*屬性上的**資料錄集**將不會顯示基礎資料提供者。

```

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 如果您的應用程式需要的資料指標服務，但您需要在基礎提供者上設定動態內容，請叫用資料指標服務之前設定的屬性。 命令物件屬性的設定一定會傳遞至基礎資料提供者，不論資料指標位置。 因此，您也可以使用命令物件設定屬性，在任何時間。

> [!NOTE]
>  動態屬性 DBPROP_SERVERDATAONINSERT 是服務不支援資料指標，即使基礎資料提供者支援。

|屬性名稱|描述|
|-------------------|-----------------|
|自動重新計算 (DBPROP_ADC_AUTORECALC)|資料錄集，這個值表示頻率建立具有 Data Shaping Service 系統會計算導出和彙總資料行。 預設值 (值 = 1) 是每當 Data Shaping Service 可讓您決定的值有變更時重新整理。 如果值為 0，一開始建立階層時，會僅會計算導出或彙總的資料行。|
|批次大小 (DBPROP_ADC_BATCHSIZE)|指出可以進行批次處理，再傳送至資料存放區的 update 陳述式數目。 批次中的多個陳述式，較少的來回行程，對資料存放區。|
|快取子資料列 (DBPROP_ADC_CACHECHILDROWS)|代表建立具有 Data Shaping Service 的資料錄集，這個值會表示子資料錄集是否會儲存在快取中供稍後使用。|
|資料指標引擎版本 (DBPROP_ADC_CEVER)|指出資料指標服務所使用的版本。|
|維護變更狀態 (DBPROP_ADC_MAINTAINCHANGESTATUS)|表示用來重新同步處理多個資料表的聯結中的一或多個資料列的命令的文字。|
|[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|指出是否應該建立索引。 當設定為 **，則為 True**，授與暫存索引以提升執行某些作業的建立。|
|[調整形狀名稱](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|表示名稱**資料錄集**。 可以是參考位於目前，或後續、 資料成形命令。|
|[重新同步命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|表示自訂命令字串，以供[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法時[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)屬性就會生效。|
|[唯一的目錄](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|表示包含所參考的資料表的資料庫名稱**唯一資料表**屬性。|
|[唯一的結構描述](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|表示所參考的資料表擁有者的名稱**唯一資料表**屬性。|
|[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|指示中的一個資料表名稱**資料錄集**建立多個資料表，就可以修改的插入、 更新或刪除。|
|更新條件 (DBPROP_ADC_UPDATECRITERIA)|中的哪些欄位會指出**其中**子句用來處理在更新期間發生的衝突。|
|[更新重新同步處理](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)(DBPROP_ADC_UPDATERESYNC)|指出是否**重新同步處理**方法會隱含地叫用後[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法 （和其行為），當**唯一資料表**屬性就會生效。|

 您也可以設定，或藉由指定其名稱為索引中擷取動態屬性**屬性**集合。 比方說，取得並列印目前的值[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)動態屬性，然後將新的值，如下所示：

```
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>內建的屬性行為
 OLE DB 資料指標服務也會影響某些內建屬性的行為。

|屬性名稱|描述|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|補充的一種可供資料指標**資料錄集**。|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|補充適用於鎖定的類型**資料錄集**。 啟用批次更新。|
|[排序](../../../ado/reference/ado-api/sort-property.md)|指定一或多個欄位名稱**資料錄集**排序，以及每個欄位以遞增或遞減順序排序。|

## <a name="method-behavior"></a>方法的行為
 OLE DB 資料指標服務啟用，或會影響的行為[欄位](../../../ado/reference/ado-api/field-object.md)物件的[附加](../../../ado/reference/ado-api/append-method-ado.md)方法，而**資料錄集**物件的[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)， [resync](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，和[儲存](../../../ado/reference/ado-api/save-method.md)方法。
