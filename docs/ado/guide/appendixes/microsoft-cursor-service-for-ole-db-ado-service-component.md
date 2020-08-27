---
description: '適用于 OLE DB (ADO 服務元件的 Microsoft 資料指標服務) '
title: 適用于 OLE DB (ADO 服務元件的 Microsoft 資料指標服務) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
author: rothja
ms.author: jroth
ms.openlocfilehash: 02eaad96593af153b1692beed4bcf846ff92ab7f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991089"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>適用于 OLE DB 的 Microsoft 資料指標服務總覽
適用于 OLE DB 的 Microsoft 資料指標服務會補充資料提供者的資料指標支援功能。 如此一來，使用者就能從所有資料提供者都感覺出相當一致的功能。

 Cursor 服務可提供動態屬性，並增強某些方法的行為。 例如， [Optimize](../../reference/ado-api/optimize-property-dynamic-ado.md) 動態屬性可建立暫存索引來加速特定作業，例如 [Find](../../reference/ado-api/find-method-ado.md) 方法。

 在所有情況下，資料指標服務都可支援批次更新。 當資料提供者只能提供較小的資料指標（例如靜態資料指標）時，它也會模擬更有能力的資料指標類型，例如動態資料指標。

## <a name="keyword"></a>關鍵字
 若要叫用此服務元件，請將 [記錄集](../../reference/ado-api/recordset-object-ado.md) 或 [連接](../../reference/ado-api/connection-object-ado.md) 物件的 [CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md) 屬性設定為 **adUseClient**。

```vb
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>動態屬性
 叫用 OLE DB 的資料指標服務時，會將下列動態屬性加入至 **記錄集** 物件的 [properties](../../reference/ado-api/properties-collection-ado.md) 集合中。 **連接**和**記錄集**物件動態屬性的完整清單會列在[ADO 動態屬性索引](../../reference/ado-api/ado-dynamic-property-index.md)中。 相關聯的 OLE DB 屬性名稱（如果有的話）會包含在 ADO 屬性名稱後面的括弧中。

 在叫用資料指標服務之後，基礎資料來源看不到某些動態屬性的變更。 例如，基礎資料提供者將看不到在**記錄集**上設定*命令逾時*屬性。

```vb

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 如果您的應用程式需要資料指標服務，但您需要在基礎提供者上設定動態屬性，請先設定屬性，然後再叫用資料指標服務。 無論資料指標位置為何，Command 物件屬性設定一律會傳遞至基礎資料提供者。 因此，您也可以隨時使用命令物件來設定屬性。

> [!NOTE]
>  資料指標服務不支援動態屬性 DBPROP_SERVERDATAONINSERT，即使基礎資料提供者支援它也一樣。

|屬性名稱|描述|
|-------------------|-----------------|
|自動重新計算 (DBPROP_ADC_AUTORECALC) |針對使用資料成形服務建立的記錄集，這個值會指出計算和匯總資料行的計算頻率。 預設 (值 = 1) 是在資料成形服務判斷值已變更時重新計算。 如果此值為0，則只會在首次建立階層時計算計算或匯總資料行。|
|批次大小 (DBPROP_ADC_BATCHSIZE) |指出在傳送至資料存放區之前可批次處理的 update 語句數目。 批次中的語句越多，資料存放區的來回行程就越少。|
|快取子資料列 (DBPROP_ADC_CACHECHILDROWS) |針對使用資料成形服務建立的記錄集，這個值會指出子記錄集是否儲存在快取中以供稍後使用。|
|資料指標引擎版本 (DBPROP_ADC_CEVER) |指出所使用的資料指標服務版本。|
|維護變更狀態 (DBPROP_ADC_MAINTAINCHANGESTATUS) |指出用來在多個資料表聯結中重新同步處理一或多個資料列的命令文字。|
|[最佳化](../../reference/ado-api/optimize-property-dynamic-ado.md)|指出是否應該建立索引。 當設為 **True**時，會授權暫時建立索引，以改善某些作業的執行。|
|[重新調整名稱](../../reference/ado-api/reshape-name-property-dynamic-ado.md)|指出 **記錄集**的名稱。 可以在目前或後續的資料成形命令中參考。|
|[Resync 命令](../../reference/ado-api/resync-command-property-dynamic-ado.md)|指出當[Unique Table](../../reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)屬性有效時，重新[同步](../../reference/ado-api/resync-method.md)處理方法所使用的自訂命令字串。|
|[唯一目錄](../../reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|指出包含 **Unique table** 屬性中所參考之資料表的資料庫名稱。|
|[唯一架構](../../reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|指出 **Unique table** 屬性中所參考之資料表的擁有者名稱。|
|[Unique Table](../../reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|表示 **記錄集** 內一個資料表的名稱，該資料表是由可透過插入、更新或刪除來修改的多個資料表所建立。|
|更新準則 (DBPROP_ADC_UPDATECRITERIA) |指出 **WHERE** 子句中的哪些欄位是用來處理更新期間發生的衝突。|
|[更新](../../reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC) 的重新同步|指出當**Unique Table**屬性有效時，重新**同步**方法是否會在[UpdateBatch](../../reference/ado-api/updatebatch-method.md)方法 (和其行為) 隱含地叫用。|

 您也可以將動態屬性指定為 **屬性** 集合的索引，藉以設定或抓取動態屬性。 例如，取得並列印 [Optimize](../../reference/ado-api/optimize-property-dynamic-ado.md) 動態屬性的目前值，然後設定新的值，如下所示：

```vb
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>內建屬性行為
 OLE DB 的資料指標服務也會影響某些內建屬性的行為。

|屬性名稱|描述|
|-------------------|-----------------|
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|補充適用于 **記錄集**的資料指標類型。|
|[LockType](../../reference/ado-api/locktype-property-ado.md)|補充適用于 **記錄集**的鎖定類型。 啟用批次更新。|
|[排序](../../reference/ado-api/sort-property.md)|指定 **記錄集** 所依據的一或多個功能變數名稱，以及每個欄位是否以遞增或遞減順序排序。|

## <a name="method-behavior"></a>方法行為
 OLE DB 的資料指標服務會啟用或影響 [Field](../../reference/ado-api/field-object.md) 物件之 [Append](../../reference/ado-api/append-method-ado.md) 方法的行為;以及 **記錄集** 物件的 [Open](../../reference/ado-api/open-method-ado-recordset.md)、 [Resync](../../reference/ado-api/resync-method.md)、 [UpdateBatch](../../reference/ado-api/updatebatch-method.md)和 [Save](../../reference/ado-api/save-method.md) 方法。