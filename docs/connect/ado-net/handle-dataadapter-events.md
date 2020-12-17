---
title: 處理 DataAdapter 事件
description: 描述 DataAdapter 事件及使用方法。
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 11515b25-ee49-4b1d-9294-a142147c1ec5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e3715f2060857bf6d5fabb37c049d6e9cff1ee40
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/16/2020
ms.locfileid: "97559210"
---
# <a name="handle-dataadapter-events"></a>處理 DataAdapter 事件

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SqlClient Data Provider for SQL Server <xref:Microsoft.Data.SqlClient.SqlDataAdapter> 會公開三個事件，供您用來回應在資料來源中對資料所做的變更。 下表說明 `DataAdapter` 事件。

|事件|描述|  
|-----------|-----------------|  
|`RowUpdating`|資料列上的 UPDATE、INSERT 或 DELETE 作業 (呼叫其中一個 `Update` 方法) 即將開始。|  
|`RowUpdated`|資料列上的 UPDATE、INSERT 或 DELETE 作業 (呼叫其中一個 `Update` 方法) 已經完成。|  
|`FillError`|`Fill` 作業過程中發生錯誤。|  

## <a name="rowupdating-and-rowupdated-events"></a>RowUpdating 與 RowUpdated 事件

在資料來源中處理 `RowUpdating` 之資料列的任何更新之前，會引發 <xref:System.Data.DataSet>。 在資料來源中處理 `RowUpdated` 之資料列的任何更新之後，會引發 `DataSet`。 所以，您可以使用 `RowUpdating` 在更新發生前修改更新行為，讓您更能控制更新發生的時間、保留對已更新資料列的參考、取消目前更新、將更新排程於稍後進行批次處理等其他功能。 `RowUpdated` 對於回應在更新期間發生的錯誤和例外狀況而言很有用。 您可以將 **錯誤資訊** 新增至 `DataSet` 以及 **重試邏輯** 等等。

傳遞至 <xref:System.Data.Common.RowUpdatingEventArgs> 和 <xref:System.Data.Common.RowUpdatedEventArgs> 事件的 `RowUpdating` 和 `RowUpdated` 引數包括下列項目：`Command` 屬性 (參考正用來執行更新的 `Command` 物件)、`Row` 屬性 (參考包含已更新資訊的 `DataRow` 物件)、`StatementType` 屬性 (正在執行該類型的更新)、`TableMapping` (如果適用)；以及作業的 `Status`。

您可以使用 `Status` 屬性來判斷作業期間是否發生錯誤，也可以依您的需要，控制目前和結果資料列的動作。 發生事件時，`Status` 屬性即等於 `Continue` 或 `ErrorsOccurred`。 您可以將 `Status` 屬性設成下列表格所顯示的值，以控制更新期間的後續動作。

|狀態|描述|  
|------------|-----------------|  
|`Continue`|繼續更新作業。|  
|`ErrorsOccurred`|中止更新作業並擲回例外狀況。|  
|`SkipCurrentRow`|忽略目前資料列並繼續更新作業。|  
|`SkipAllRemainingRows`|中止更新作業但不擲回例外狀況。|  

若將 `Status` 屬性設為 `ErrorsOccurred`，則會擲回例外狀況。 您可以將 `Errors` 屬性設定為您希望的例外狀況，以控制擲回的例外狀況。 若將 `Status` 設為其他任一值，則可避免擲回例外狀況。

您也可以使用 `ContinueUpdateOnError` 屬性來處理更新資料列的錯誤。 如果 `DataAdapter.ContinueUpdateOnError` 為 `true`，則當資料列的更新造成擲回例外狀況時，會將例外狀況的文字放入特定資料列的 `RowError` 資訊中，並繼續作業，而不擲回例外狀況。 這樣一來，您就可以在完成 `Update` 後才回應錯誤，而 `RowUpdated` 事件則是讓您在發生錯誤時立即回應該錯誤。

下列程式碼範例顯示如何加入和移除事件處理常式。 `RowUpdating` 事件處理常式將所有的刪除記錄和時間戳記寫入記錄檔。 `RowUpdated` 事件處理常式會將錯誤資訊新增至 `DataSet` 內資料列的 `RowError` 屬性中、隱藏例外狀況，並繼續作業 (與 `ContinueUpdateOnError` = `true` 的行為相同)。

[!code-csharp[SqlDataAdapter_Events#1](~/../sqlclient/doc/samples/SqlDataAdapter_Events.cs#1)]

## <a name="fillerror-event"></a>FillError 事件

`DataAdapter` 作業期間發生錯誤時，`FillError` 會發出 `Fill` 事件。 當新增的資料列資料必須放棄一些精確度，否則無法轉換為 .NET 類型時，通常就會發生這類型的錯誤。

`Fill` 作業期間如果發生錯誤，則不會將目前的資料列加入 `DataTable`。 `FillError` 事件可讓您解析錯誤並加入資料列，或忽略排除的資料列，繼續進行 `Fill` 作業。

傳遞給 <xref:System.Data.FillErrorEventArgs> 事件的 `FillError` 可包含數個屬性，讓您回應並解決錯誤。 下列表格顯示 `FillErrorEventArgs` 物件的屬性。

|屬性|描述|  
|--------------|-----------------|  
|`Errors`|所發生的 `Exception`。|  
|`DataTable`|發生錯誤時，填入的 `DataTable` 物件。|  
|`Values`|發生錯誤時，包含加入資料列值的物件陣列。 `Values` 陣列的序數參考對應至加入資料列資料行的序數參考。 例如，`Values[0]` 便是當成資料列第一個資料行而加入的值。|  
|`Continue`|可讓您選擇是否要擲回例外狀況。 將 `Continue` 屬性設為 `false`，即可中斷目前的 `Fill` 作業，並擲回例外狀況。 將 `Continue` 設為 `true`，則不管是否發生錯誤，都將繼續進行 `Fill` 作業。|  

下列程式碼範例針對 `FillError` 的 `DataAdapter` 事件，加入事件處理常式。 範例的 `FillError` 事件程式碼會在有機會回應例外狀況時，判斷是否可能會缺少精確度。

[!code-csharp[SqlDataAdapter_Events#2](~/../sqlclient/doc/samples/SqlDataAdapter_Events.cs#2)]

## <a name="see-also"></a>請參閱

- [DataAdapter 和 DataReader](dataadapters-datareaders.md)
- [事件](/dotnet/standard/events/index)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
