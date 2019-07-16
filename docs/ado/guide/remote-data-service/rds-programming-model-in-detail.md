---
title: RDS 程式設計模型詳述 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d7251e3a403168e8383e636a8e6b5f712b9f7bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922521"
---
# <a name="rds-programming-model-in-detail"></a>RDS 程式設計模型詳述
RDS 程式設計模型的重要元素如下：  
  
-   RDS.DataSpace  
  
-   RDSServer.DataFactory  
  
-   RDS.DataControl  
  
-   Event - 事件  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 伺服器與要叫用伺服器程式，必須指定用戶端應用程式。 您的應用程式會接收伺服器程式的參考，並可以視為參考，如同它是伺服器程式本身。  
  
 RDS 物件模型包含這項功能與[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)物件。  
  
 伺服器程式指定的程式識別項或*ProgID*。 伺服器會使用*ProgID*和伺服器電腦的登錄，以找出實際的程式，以起始的相關資訊。  
  
 RDS 可讓內部根據伺服器程式透過網際網路或近端內部網路; 是否在遠端伺服器上的差異在伺服器上區域網路上;或不是，伺服器上，但改為在本機的動態連結程式庫 (DLL)。 這項區別會決定如何資訊的用戶端與伺服器之間交換位置，並讓參考傳回給用戶端應用程式的型別上的實際差異。 不過，從您的觀點來看，這項區別會有任何特殊的意義。 最重要的是，您會收到可用的程式參考。  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 RDS 提供預設的伺服器程式，可以執行資料來源並傳回的 SQL 查詢[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或採取**資料錄集**物件，並更新資料來源。  
  
 RDS 物件模型包含這項功能與[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件。  
  
 此外，此物件具有方法來建立空**資料錄集**您可以透過程式設計方式填入的物件 ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md))，而且另一個轉換的方法**資料錄集**物件為文字字串，以建置網頁 ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md))。  
  
 使用 ADO 時，您可以覆寫一些標準的連接和命令行為**RDSServer.DataFactory**具有**DataFactory**處理常式和自訂檔案，其中包含連接命令時，和安全性參數。  
  
 伺服器程式有時也稱為*商務物件*。 您可以撰寫自己的自訂商務物件可以執行複雜的資料存取、 驗證檢查，等等。 即使在撰寫自訂商務物件，您可以建立的執行個體**RDSServer.DataFactory**物件，並使用它的一些方法來完成您自己的工作。  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 RDS 提供一個方法來結合的功能**rds。DataSpace**並**RDSServer.DataFactory**，也可啟用視覺控制項，以輕鬆地使用**資料錄集**查詢所傳回之資料來源的物件。 RDS 嘗試最常見的情況下，要盡量以自動取得的存取權的伺服器上的資訊，並顯示在視覺控制項。  
  
 RDS 物件模型包含這項功能與[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 **Rds。DataControl**具有兩個層面。 其中一個層面是關於資料來源。 如果您設定的命令和使用的連接資訊**Connect**並**SQL**的屬性**rds。DataControl**，它會自動使用**rds。DataSpace**來建立預設值的參考**RDSServer.DataFactory**物件。 然後**RDSServer.DataFactory**會使用**Connect**屬性值連接到資料來源，請使用**SQL**屬性的值，以取得**資料錄集**從資料來源，並傳回**Recordset**物件**rds。DataControl**。  
  
 第二個層面相關的顯示方式傳回**資料錄集**視覺控制項中的資訊。 您可以建立關聯的視覺控制項**rds。DataControl** （在程序，稱為繫結），以及存取中相關聯的資訊**資料錄集**物件，在 Microsoft® Internet Explorer 的網頁上顯示查詢結果。 每個**rds。DataControl**物件繫結其中一個**資料錄集**物件，代表一或多個視覺控制項，（例如文字方塊、 下拉式方塊、 方格控制項等等） 的單一查詢的結果。 可能有多個**rds。DataControl**每個頁面上的物件。 每個**rds。DataControl**物件可以連接到不同的資料來源，而且包含個別查詢的結果。  
  
 **Rds。DataControl**物件也有它自己的方法，來瀏覽、 排序和篩選相關聯的資料列**資料錄集**物件。 這些方法很相似，但不同的方法，在 ADO**資料錄集**物件。  
  
## <a name="events"></a>Events  
 RDS 可支援兩個本身的 ADO 事件模型無關的事件。 [OnReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md)事件會被呼叫時**rds。DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)屬性變更，藉此非同步作業已順利完成，通知您終止，或發生錯誤。 [OnError](../../../ado/reference/rds-api/onerror-event-rds.md)事件每次錯誤發生時，即使呼叫非同步作業期間發生錯誤。  
  
> [!NOTE]
>  Microsoft Internet Explorer 至 RDS 提供兩個額外的事件： **onDataSetChanged**，這表示**Recordset**是功能，但仍然擷取資料列，和**onDataSetComplete**，這表示**資料錄集**完成擷取資料列。  
  
## <a name="see-also"></a>另請參閱  
 [物件的 RDS 程式設計模型](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace 物件 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



