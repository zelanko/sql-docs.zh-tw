---
title: "RDS 程式設計模型，在詳細資料 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e3edfd1b1ec33d4c014fae4a0fed8d61d5ef8ed
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="rds-programming-model-in-detail"></a>在詳細資料的 RDS 程式設計模型
RDS 的程式設計模型的重要元素如下：  
  
-   RDS資料空間  
  
-   RDSServer.DataFactory  
  
-   RDSDataControl  
  
-   事件  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="rdsdataspace"></a>RDS資料空間  
 用戶端應用程式必須指定伺服器和伺服器方案，來叫用。 傳回，您的應用程式接收伺服器程式的參考，並可以視為參考，就好像伺服器程式本身。  
  
 RDS 物件模型意這項功能與[.RDSDataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)物件。  
  
 伺服器程式指定的程式識別項或*ProgID*。 伺服器會使用*ProgID*和伺服器電腦的登錄，以找出實際啟動程式的相關資訊。  
  
 RDS 會在內部根據伺服器程式透過網際網路或內部網路; 是否在遠端伺服器上的差異在伺服器上區域網路上。不在或伺服器，而是在本機的動態連結程式庫 (DLL)。 這個區別決定如何在用戶端與伺服器之間交換和資訊的明確的差異，在於參考傳回給用戶端應用程式的型別。 不過，從您的觀點，這樣的區別有沒有特殊意義。 所有會影響結果是您接收的可程式參照。  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 RDS 提供可以執行的 SQL 查詢的資料來源和傳回的預設伺服器程式[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或採取**資料錄集**物件，並更新資料來源。  
  
 RDS 物件模型意這項功能與[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件。  
  
 此外，此物件具有方法來建立一個空**資料錄集**物件，您可以透過程式設計方式填 ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md))，而且另一個轉換方法**資料錄集**物件來建立的 Web 網頁的文字字串 ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md))。  
  
 使用 ADO 時，您可以覆寫一些標準的連接和命令行為**RDSServer.DataFactory**與**DataFactory**處理常式和自訂檔案，其中包含連接命令時，和安全性參數。  
  
 伺服器程式有時也稱為*商務物件*。 您可以撰寫自己的自訂商務物件，可以執行複雜的資料存取、 有效性檢查等等。 即使在撰寫自訂的商務物件，您可以建立的執行個體**RDSServer.DataFactory**物件，並使用其中一些方法來完成您自己的工作。  
  
## <a name="rdsdatacontrol"></a>RDSDataControl  
 RDS 提供方法來結合的功能**.RDSDataSpace**和**RDSServer.DataFactory**，而且可讓視覺控制項能夠輕鬆使用**資料錄集**資料來源的查詢所傳回的物件。 RDS 嘗試最常見的情況下，執行最多可達能夠自動存取的伺服器上的資訊，並顯示視覺控制項中。  
  
 RDS 物件模型意這項功能與[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 **.RDSDataControl**具有兩個層面。 其中一個層面都屬於資料來源。 如果您設定的命令和連接資訊使用**連接**和**SQL**屬性**.RDSDataControl**，便會自動使用**.RDSDataSpace**建立預設參考**RDSServer.DataFactory**物件。 然後在**RDSServer.DataFactory**將使用**連接**屬性值設定為連接到資料來源，請使用**SQL**屬性值，以取得**資料錄集**從資料來源，並傳回**資料錄集**物件**.RDSDataControl**。  
  
 第二個層面相關的顯示傳回**資料錄集**視覺控制項中的資訊。 您可以建立關聯的視覺控制項**.RDSDataControl** （在稱為繫結程序），以及相關聯的資訊存取**資料錄集**物件，在 Microsoft® Internet Explorer 中網頁上顯示查詢結果。 每個**.RDSDataControl**物件將繫結其中一個**資料錄集**代表一或多個視覺控制項，（例如文字方塊、 下拉式方塊、 方格控制項等） 的單一查詢，結果的物件。 可能有多個**.RDSDataControl**每個頁面上的物件。 每個**.RDSDataControl**物件可以連接到不同的資料來源，包含個別查詢的結果。  
  
 **.RDSDataControl**物件都有它自己的巡覽、 排序和篩選相關聯的資料列的方法**資料錄集**物件。 這些方法很相似，但不是相同的方法上之 ADO**資料錄集**物件。  
  
## <a name="events"></a>事件  
 RDS 支援兩個其本身的 ADO 事件模型無關的事件。 [OnReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md)事件被呼叫時**.RDSDataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)屬性變更，因此當非同步作業已成功完成時，通知您終止，或發生錯誤。 [OnError](../../../ado/reference/rds-api/onerror-event-rds.md)事件在錯誤情況下，即使呼叫非同步作業期間發生錯誤。  
  
> [!NOTE]
>  Microsoft Internet Explorer 提供兩個額外的事件至 RDS: **onDataSetChanged**，這表示**資料錄集**是功能，但仍然擷取資料列，以及**onDataSetComplete**，這表示**資料錄集**完成擷取資料列。  
  
## <a name="see-also"></a>請參閱  
 [RDS 與物件的程式設計模型](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [資料空間物件 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



