---
title: SQL Server 中的資料庫鏡像
description: 描述資料庫鏡像功能。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 38481625645a7d2a70b7d3212cdf9ef765ca9c1f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928864"
---
# <a name="database-mirroring-in-sql-server"></a>SQL Server 中的資料庫鏡像

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 中的資料庫鏡像可讓您將 SQL Server 資料庫的複本或鏡像保存在待命伺服器上。 鏡像可確保隨時都有兩個個別的資料複本，進而提供高可用性與完整的資料備援能力。 SQL Server 的 Microsoft SqlClient 提供者提供對資料庫鏡像的隱含支援，這樣將其設定給 SQL Server 資料庫後，則開發人員無需採取任何動作或撰寫任何程式碼。 此外，<xref:Microsoft.Data.SqlClient.SqlConnection> 物件支援可在 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> 中提供容錯移轉夥伴伺服器名稱的明確連線模式。  
  
下列簡化的事件順序會針對 <xref:Microsoft.Data.SqlClient.SqlConnection> 物件發生，此物件會以設定為用於鏡像的資料庫作為目標：  
  
1. 用戶端應用程式成功連線到主體資料庫，而伺服器會傳回夥伴伺服器的名稱，接著夥伴伺服器名稱會在用戶端上快取。  
  
2. 如果包含主體資料庫的伺服器失敗或連線中斷，連線和交易狀態就會遺失。 用戶端應用程式嘗試重新建立與主體資料庫的連線，但失敗。  
  
3. 然後，用戶端應用程式會以透明方式，嘗試建立與夥伴伺服器上鏡像資料庫的連線。 如果成功，會將連線重新導向至鏡像資料庫，接著鏡像資料庫會成為新的主體資料庫。  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>在連接字串中指定容錯移轉夥伴  
如果您在連接字串中提供容錯移轉夥伴伺服器的名稱，當用戶端應用程式第一次連接時，如果主體資料庫無法使用，用戶端將會以透明方式嘗試與容錯移轉夥伴連線。  
  
```csharp
";Failover Partner=PartnerServerName"  
```  
  
如果您省略容錯移轉夥伴伺服器的名稱，而且當用戶端應用程式第一次連線時主體資料庫無法使用，則會引發 <xref:Microsoft.Data.SqlClient.SqlException>。  
  
成功開啟 <xref:Microsoft.Data.SqlClient.SqlConnection> 之後，伺服器就會傳回容錯移轉夥伴名稱，並取代連接字串中提供的任何值。  
  
> [!NOTE]
>  您必須在資料庫鏡像案例的連接字串中，明確指定初始目錄或資料庫名稱。 如果用戶端在沒有明確指定初始目錄或資料庫的連線上收到容錯移轉資訊，則不會快取該容錯移轉資訊，且應用程式在主體伺服器失敗時不會嘗試容錯移轉。 如果連接字串內含容錯移轉夥伴的值，但是沒有初始目錄或資料庫的值，就會引發 `InvalidArgumentException`。  
  
## <a name="retrieving-the-current-server-name"></a>擷取目前的伺服器名稱  
萬一發生容錯移轉，您可以使用 <xref:Microsoft.Data.SqlClient.SqlConnection> 物件的 <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> 屬性，擷取目前連線實際連接的伺服器名稱。 假設連接變數參考已開啟的 <xref:Microsoft.Data.SqlClient.SqlConnection>，下列程式碼片段就會擷取使用中伺服器的名稱。  
  
當發生容錯移轉事件且連線切換到鏡像伺服器時，**DataSource** 屬性會更新以反映鏡像名稱。  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>SqlClient 鏡像行為  
用戶端一律會嘗試連線到目前的主體伺服器。 如果失敗，會嘗試容錯移轉夥伴。 如果鏡像資料庫已經切換到夥伴伺服器上的主體角色，連線就會成功，而且新的主體-鏡像對應會傳送至用戶端，並在呼叫 <xref:System.AppDomain> 的存留期間進行快取。 該項目並非儲存於永續性儲存區中，而且無法在不同 **AppDomain** 或處理序中的後續連線上使用。 不過，其可在相同 **AppDomain** 內的後續連線上使用。 請注意，在相同或不同電腦上執行的其他 **AppDomain** 或處理序永遠擁有自己的連線集區，並且不會重設那些連線。 在此情況下，如果主要資料庫關閉，則每個處理序或 **AppDomain** 會失敗一次，且會自動清除集區。  
  
> [!NOTE]
>  伺服器上的鏡像支援是以個別資料庫為基礎所設定的。 如果是針對不包含在主體/鏡像集內的其他資料庫執行資料操作作業，不論是使用多部分名稱或透過變更目前的資料庫，這些對其他資料庫所做的變更都不會在發生失敗時傳播。 在未鏡像的資料庫中修改資料時，並不會產生任何錯誤。 開發人員必須評估此類作業可能產生的影響。  
  
## <a name="next-steps"></a>後續步驟
### <a name="database-mirroring-resources"></a>資料庫鏡像資源  
如需設定、部署和管理鏡像的概念文件和詳細資訊，請參閱 SQL Server 文件中的下列資源。  
  
|資源|描述|  
|--------------|-----------------|  
|[資料庫鏡像](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)|描述如何在 SQL Server 中設定鏡像。|  
