---
title: OLE DB （ADO 服務元件） 的 Microsoft 資料指標服務 |Microsoft 文件
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
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 838c1b75d93c6a357f6b8ce706f8d444f6054703
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>Microsoft 資料指標服務的 OLE DB 概觀
OLE DB 的資料指標審查補充資料提供者的資料指標支援函數。 如此一來，使用者會感知相當一致的功能，從所有資料提供者。

 資料指標服務可提供動態內容，並增強特定方法的行為。 例如，[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)動態屬性可讓建立暫存索引以利於進行某些作業，例如[尋找](../../../ado/reference/ado-api/find-method-ado.md)方法。

 資料指標服務可提供批次更新在所有情況下支援。 資料提供者只可以提供較不支援的資料指標，例如靜態資料指標時，它也會模擬更適用的資料指標類型，例如動態資料指標。

## <a name="keyword"></a>關鍵字
 若要叫用此服務元件時，設定[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性**adUseClient**。

```
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>動態屬性
 叫用的 OLE DB 資料指標服務時，已加入下列的動態屬性**資料錄集**物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。 完整清單**連接**和**資料錄集**物件的動態屬性會列在[ADO 動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)。 相關聯的 OLE DB 屬性名稱，適用時，會包含在括號之後的 ADO 屬性名稱。

 變更一些動態內容看不到基礎資料來源叫用資料指標服務之後。 例如，設定*命令逾*屬性**資料錄集**將不會顯示基礎資料提供者。

```

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 如果您的應用程式需要的資料指標服務，但您需要設定基礎提供者上的動態屬性，請叫用資料指標服務之前設定的屬性。 命令物件的屬性設定為永遠會傳遞至基礎資料提供者，不論資料指標位置。 因此，您也可以使用命令物件設定的屬性，在任何時間。

> [!NOTE]
>  動態屬性 DBPROP_SERVERDATAONINSERT 不支援資料指標服務，即使基礎資料提供者支援它。

|屬性名稱|Description|
|-------------------|-----------------|
|自動重新計算 (DBPROP_ADC_AUTORECALC)|建立 Data Shaping Service 的這個值表示頻率的資料錄集的計算和彙總資料行被計算的。 預設值 (值 = 1) 是 Data Shaping Service 判斷的值已變更時重新計算。 如果值為 0，計算或彙總的資料行只會計算一開始建立階層時。|
|批次大小 (DBPROP_ADC_BATCHSIZE)|表示可以再傳送至資料存放區中批次處理的 update 陳述式數目。 批次中的多個陳述式，儲存的資料較少的來回行程。|
|快取子資料列 (DBPROP_ADC_CACHECHILDROWS)|建立 Data Shaping Service 與資料錄集，這個值表示子資料錄集是否會儲存在快取供稍後使用。|
|資料指標引擎版本 (DBPROP_ADC_CEVER)|表示目前使用的資料指標服務的版本。|
|維護變更狀態 (DBPROP_ADC_MAINTAINCHANGESTATUS)|表示用來重新同步處理多個資料表的聯結中的一個或多個資料列的命令文字。|
|[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|指出是否應該建立索引。 當設定為**True**，授與暫存索引以改善執行的特定作業的建立。|
|[重繪名稱](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|表示名稱**資料錄集**。 可以是參考目前中或之後，資料成形命令。|
|[重新同步處理命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|表示所使用的自訂命令字串[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法時[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)屬性就會生效。|
|[唯一的目錄](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|表示包含所參考的資料表之資料庫的名稱**唯一資料表**屬性。|
|[唯一的結構描述](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|指出所參考的資料表的擁有者名稱**唯一資料表**屬性。|
|[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|表示一個資料表中的名稱**資料錄集**建立多個資料表，就可以修改的插入、 更新或刪除。|
|更新條件 (DBPROP_ADC_UPDATECRITERIA)|指出哪一個欄位中**其中**子句用來處理更新期間發生的衝突。|
|[更新的重新同步處理](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)(DBPROP_ADC_UPDATERESYNC)|指出是否**重新同步處理**之後會隱含地叫用方法[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法 （和其行為），當**唯一資料表**屬性就會生效。|

 您也可以設定或擷取動態屬性，藉由指定其名稱為的索引**屬性**集合。 例如，取得和目前的值列印[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)動態屬性，然後將新的值，如下所示：

```
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>內建屬性行為
 OLE DB 資料指標服務也會影響某些內建屬性的行為。

|屬性名稱|Description|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|補充適用於資料指標的類型**資料錄集**。|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|補充適用於鎖定的類型**資料錄集**。 啟用批次更新。|
|[排序](../../../ado/reference/ado-api/sort-property.md)|指定一或多個欄位名稱**資料錄集**排序，以及每個欄位以遞增或遞減順序排序。|

## <a name="method-behavior"></a>方法的行為
 OLE DB 資料指標服務啟用，或會影響行為[欄位](../../../ado/reference/ado-api/field-object.md)物件的[附加](../../../ado/reference/ado-api/append-method-ado.md)方法; 而**資料錄集**物件的[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)，[重新同步處理](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，和[儲存](../../../ado/reference/ado-api/save-method.md)方法。
