---
description: RDS 程式設計模型詳述
title: RDS 程式設計模型詳細資料 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
author: rothja
ms.author: jroth
ms.openlocfilehash: af1b575f642159cad84d0ce833bb783cf2363701
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977969"
---
# <a name="rds-programming-model-in-detail"></a>RDS 程式設計模型詳述
以下是 RDS 程式設計模型的重要元素：  
  
-   RDS.DataSpace  
  
-   RDSServer.DataFactory  
  
-   RDS.DataControl  
  
-   事件  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 您的用戶端應用程式必須指定要叫用的伺服器和伺服器程式。 然後，您的應用程式會收到伺服器程式的參考，並且可以將參考視為伺服器程式本身。  
  
 RDS 物件模型將這種功能提供給 [rds。空間](../../reference/rds-api/dataspace-object-rds.md) 物件。  
  
 伺服器程式是以程式識別碼或 *ProgID*指定。 伺服器會使用 *ProgID* 和伺服器電腦的登錄來找出要起始的實際程式的相關資訊。  
  
 根據伺服器程式是在網際網路或內部網路的遠端伺服器上，RDS 會在內部進行區別。區域網路上的伺服器;或不在伺服器上，而是在本機動態程式庫 (DLL) 。 這項區別決定了在用戶端與伺服器之間交換資訊的方式，並在傳回給用戶端應用程式的參考類型之間有實質差異。 不過，從您的觀點來看，這種區別沒有特殊意義。 重要的是，您會收到可使用的程式參考。  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 RDS 提供預設的伺服器程式，可以針對資料來源執行 SQL 查詢，並傳回 [記錄集](../../reference/ado-api/recordset-object-ado.md) 物件或 **取得記錄集** 物件，並更新資料來源。  
  
 RDS 物件模型將這種功能與 [RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) 物件結合在一起。  
  
 此外，這個物件也有一個方法可建立空的 **記錄集** 物件，您可以用程式設計的方式填入 ([CreateRecordset](../../reference/rds-api/createrecordset-method-rds.md)) ，以及另一個將 **記錄集** 物件轉換成文字字串以建立網頁的方法 ([ConvertToString](../../reference/rds-api/converttostring-method-rds.md)) 。  
  
 利用 ADO，您可以使用**DataFactory**處理常式和包含連接、命令和安全性參數的自訂檔案，覆寫**RDSServer DataFactory**的一些標準連接和命令列為。  
  
 伺服器程式有時稱為 *商務物件*。 您可以撰寫自己的自訂商務物件，它可以執行複雜的資料存取、有效性檢查等等。 即使在撰寫自訂商務物件時，您也可以建立 **RDSServer DataFactory** 物件的實例，並使用其一些方法來完成您自己的工作。  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 RDS 提供結合 Rds 功能的方法 **。資料空間** 和 **RDSServer DataFactory**，也可讓視覺效果控制項輕鬆地使用資料來源的查詢所傳回的 **記錄集** 物件。 針對最常見的情況，RDS 嘗試盡可能盡可能地自動存取伺服器上的資訊，並將其顯示在視覺控制項中。  
  
 RDS 物件模型將這種功能提供給 [rds。DataControl](../../reference/rds-api/datacontrol-object-rds.md) 物件。  
  
 **RDS。DataControl**有兩個層面。 其中一個層面與資料來源有關。 如果您使用 RDS 的 **Connect** 和 **SQL** 屬性來設定命令和連接資訊 **。DataControl**，它會自動使用 **RDS。** 用來建立預設 **RDSServer. DataFactory** 物件之參考的空間。 然後， **RDSServer** 會使用 **connect** 屬性值連接到資料來源，使用 **SQL** 屬性值從資料來源取得 **記錄集** ，並將 **記錄集** 物件傳回給 **RDS。DataControl**。  
  
 第二個層面與視覺化控制項中傳回的 **記錄集** 資訊的顯示有關。 您可以將視覺效果控制項與 RDS 產生關聯 **。** 在稱為系結) 的進程中 DataControl (，並取得相關聯 **記錄集** 物件中資訊的存取權，在 Microsoft® Internet Explorer 的網頁上顯示查詢結果。 每個 **RDS。DataControl** 物件會將一個 **記錄集** 物件（代表單一查詢的結果）系結至一或多個視覺控制項 (例如文字方塊、下拉式方塊、方格控制項等) 。 可能有一個以上 **的 RDS。** 每個頁面上的 DataControl 物件。 每個 **RDS。DataControl** 物件可以連接至不同的資料來源，並包含個別查詢的結果。  
  
 **RDS。DataControl**物件也有自己的方法，可供流覽、排序及篩選關聯的**記錄集**物件的資料列。 這些方法很類似，但與 ADO **記錄集** 物件上的方法不同。  
  
## <a name="events"></a>事件  
 RDS 支援它自己的兩個事件，這與 ADO 事件模型無關。 每當 RDS 時，就會呼叫 [onReadyStateChange](../../reference/rds-api/onreadystatechange-event-rds.md) 事件 **。DataControl** [ReadyState](../../reference/rds-api/readystate-property-rds.md) 屬性變更，因此會在非同步作業已順利完成、終止或發生錯誤時通知您。 只要發生錯誤，就會呼叫 [onError](../../reference/rds-api/onerror-event-rds.md) 事件，即使是在非同步作業期間發生錯誤。  
  
> [!NOTE]
>  Microsoft Internet Explorer 針對 RDS： **onDataSetChanged**提供兩個額外的事件，這表示 **記錄集** 可以正常運作，但仍在抓取資料列和 **OnDataSetComplete**，這表示 **記錄集** 已完成資料列的取出。  
  
## <a name="see-also"></a>另請參閱  
 [具有物件的 RDS 程式設計模型](./rds-programming-model-with-objects.md)   
 [DataControl 物件 (RDS) ](../../reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 物件 (RDSServer) ](../../reference/rds-api/datafactory-object-rdsserver.md)   
 [ (RDS) 的空間物件 ](../../reference/rds-api/dataspace-object-rds.md)   
 [RDS 案例](./rds-scenario.md)   
 [RDS 教學課程](./rds-tutorial.md)   
 [RDS 使用方式與安全性](./rds-usage-and-security.md)