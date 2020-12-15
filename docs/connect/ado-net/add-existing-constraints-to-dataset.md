---
title: 將現有條件約束加入至資料集
description: 描述如何將現有的條件約束新增至 DataSet。
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 307d2809-208b-4cf8-b6a9-5d16f15fc16c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 9471f62c36604cb01ea78f558ac3bfbcb7f4bc01
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772211"
---
# <a name="add-existing-constraints-to-a-dataset"></a>將現有條件約束加入至資料集

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

<xref:Microsoft.Data.SqlClient.SqlDataAdapter> 的 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 方法只使用來自資料來源的資料表資料行和資料列填入 <xref:System.Data.DataSet>；雖然條件約束一般是由資料來源所設定，但 **Fill** 方法預設不會將這個結構描述資訊新增至 **DataSet**。

若要以資料來源的現有主索引鍵條件約束資訊填入 **DataSet**，您可以呼叫 **DataAdapter** 的 <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> 方法，或在呼叫 **Fill** 前先將 **DataAdapter** 的 <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> 屬性設定為 **AddWithKey**。 這樣能確保 **DataSet** 內的主索引鍵條件約束反映出資料來源內的主索引鍵條件約束。

> [!NOTE]
> 不包含外部索引鍵條件約束資訊，且必須明確建立。

將資料填入 **DataSet** 前先將結構描述資訊新增至其中，便能確保 **DataSet** 內的 <xref:System.Data.DataTable> 物件包含主索引鍵條件約束。 這麼一來，再次呼叫以填入 **DataSet** 時，便會使用主索引鍵資料行資訊來比對資料來源的新資料列和每個 **DataTable** 中的目前資料列，然後以資料來源的資料覆寫資料表中的目前資料。 若無結構描述資訊，則來自資料來源的新資料列會附加至 **DataSet**，而造成資料列重複。

> [!NOTE]
> 如果資料來源中的資料行定義為自動遞增，則 <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> 方法或 <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> 為 **AddWithKey** 的 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 方法，會建立 **DataColumn**，並將其 **AutoIncrement** 屬性設為 `true`。 但是您必須自行設定 **AutoIncrementStep** 和 **AutoIncrementSeed** 的值。

> [!NOTE]
> 若您使用 **FillSchema** 或將 **MissingSchemaAction** 設定為 **AddWithKey**，則資料來源需要進行其他的作業來判斷主索引鍵資料行資訊。 這些其他作業可能會降低效能。 如果您在設計階段就已知道主索引鍵資訊，建議您明確地指定主索引鍵資料行，以達到最佳效能。

下列程式碼範例示範如何使用 <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> 將結構描述資訊新增至 **DataSet**：

[!code-csharp[SqlDataAdapter_FillDataSet#1](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#1)]

下列程式碼範例示範如何使用 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 方法與 <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> 屬性將結構描述資訊新增至 **DataSet**：

[!code-csharp[SqlDataAdapter_FillDataSet#2](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#2)]

## <a name="handling-multiple-result-sets"></a>處理多個結果集

如果 **DataAdapter** 發現從 <xref:Microsoft.Data.SqlClient.SqlDataAdapter.SelectCommand%2A> 傳回的多個結果集，便會在 **DataSet** 內建立多個資料表。 會給予資料表一個以零為底數的 **Table** *N* 增量預設名稱，並從 **Table** 開始，而非 "Table0"。 如果資料表名稱作為引數傳遞至 <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> 方法，則會給予資料表一個以零為底數的 **TableName** *N* 增量名稱，並從 **TableName** 開始，而非 "TableName0"。

## <a name="see-also"></a>請參閱

- [DataAdapter 和 DataReader](dataadapters-datareaders.md)
- [在 ADO.NET 中擷取及修改資料](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
