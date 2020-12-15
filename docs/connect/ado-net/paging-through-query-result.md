---
title: 逐頁查看查詢結果
description: 提供以資料分頁形式檢視查詢結果的範例。
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: fa360c46-e5f8-411e-a711-46997771133d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 2de305e1069964f2d1a67b7f201578c7448d3e09
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772184"
---
# <a name="paging-through-a-query-result"></a>逐頁查看查詢結果

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

將查詢結果分頁是以較小資料子集或頁傳回查詢結果的過程。 這是一種常用的方式，可將結果以小型、易於管理的區塊顯示給使用者。

<xref:Microsoft.Data.SqlClient.SqlDataAdapter> 可讓您輕鬆地從多載的 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 方法中僅傳回一頁資料。 不過，如需對大筆查詢結果進行分頁，則這種方式可能不是最好的選擇，因為雖然 **DataAdapter** 只會將要求的記錄填入目標 <xref:System.Data.DataTable> 或 <xref:System.Data.DataSet>，但仍然會用到傳回整個查詢所需的資源。

若您要從資料來源傳回一頁資料，並且不使用傳回整個查詢的資源，請為您的查詢指定其他準則，以將傳回的資料列縮小到必要的範圍內。

若要使用 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 方法傳回資料頁，請針對資料頁中的第一筆記錄指定 **startRecord** 參數，再針對資料頁中的記錄數目指定 **maxRecords** 參數。

## <a name="example"></a>範例

下列程式碼範例示範如何使用 <xref:System.Data.Common.DbDataAdapter.Fill%2A> 方法傳回查詢結果的第一頁，其頁面大小為五筆記錄。

[!code-csharp[SqlDataAdapter_Paging#1](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#1)]

前一個範例中，**DataSet** 只填入了五筆記錄，但是傳回了整個 **Orders** 資料表。 若要以相同的五筆記錄填入 **DataSet**，但是只傳回五筆記錄，請在您的 SQL 陳述式使用 `TOP` 與 `WHERE` 子句，如下列範例所示。

[!code-csharp[SqlDataAdapter_Paging#2](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#2)]

> [!NOTE]
> 以這種方式逐頁瀏覽查詢結果時，您必須保留排序資料列的 `unique identifier`，以便將唯一識別碼傳遞至命令，以傳回下一頁的記錄，如下列程式碼範例所示。

[!code-csharp[SqlDataAdapter_Paging#4](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#4)]

若要透過採用 **startRecord** 和 **maxRecords** 參數的多載 **Fill** 方法來傳回 `next page of records`，請按頁面大小來遞增目前的記錄索引，並填入資料表。

> [!NOTE]
> 請記住，雖然只是在 **DataSet** 中新增一頁記錄，但實際上資料庫伺服器會傳回整個查詢結果。

下列程式碼範例中，資料表列會先經過清除後，再填入下一頁資料。 您可以在本機快取中保留特定數量的傳回資料列，來降低往返資料庫伺服器的次數。

[!code-csharp[SqlDataAdapter_Paging#3](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#3)]

若要在資料庫伺服器不傳回整個查詢的情況下，傳回下一頁記錄，請對 SELECT 陳述式指定限制準則。 由於前面的範例保留了最後傳回的記錄，因此您可以在 WHERE 子句使用它來指定查詢的起始點，如下列範例所示。

[!code-csharp[SqlDataAdapter_Paging#5](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#5)]

## <a name="see-also"></a>請參閱

- [DataAdapter 和 DataReader](dataadapters-datareaders.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
