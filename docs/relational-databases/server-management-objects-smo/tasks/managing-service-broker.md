---
title: 管理 Service Broker |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Service Broker [SMO]
ms.assetid: b29d7432-d1e5-4bb6-b544-57b3a9430f95
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1759ec9e89f53a224abd73a742d4c7dbaaeffe61
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148423"
---
# <a name="managing-service-broker"></a>管理 Service Broker

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  在 SMO 中, [!INCLUDE[ssSB](../../../includes/sssb-md.md)]您可以在**microsoft. sqlserver** . d a d namespace 命名空間中找到物件, 而這需要參考 microsoft. sqlserver .dll。 支援類別資訊也需要參考 Microsoft.SqlServer.ServiceBrokerEnum.dll。  
  
 SMO 會提供一組 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 物件，允許 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 的程式設計管理 (DDL) 實作。 這包括定義訊息類型、合約、佇列與服務。 SMO 是一個其用途並不在於資料操作的管理工具，因此，SMO 不支援傳送和接收 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 訊息。  
  
 在 SMO 中，<xref:Microsoft.SqlServer.Management.Smo.Database.ServiceBroker%2A> 物件是最上層的類別，其下則為所有 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 功能所在之處。 對於參與分散式訊息應用程式的每個資料庫而言，都需要 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 實作。 因此，<xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceBroker> 物件是 <xref:Microsoft.SqlServer.Management.Smo.Database> 物件的子系。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceBroker> 物件包含下列物件的集合，用於定義 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 實作：  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Broker.MessageType> 物件代表定義訊息內容的訊息類型。  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Broker.MessageTypeMapping> 物件代表指定給定交談中訊息方向和類型的合約。  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceQueue> 物件會在傳送訊息前以及收到訊息後儲存訊息。 它們提供服務之間的非同步通訊，以及其他優點，如自動鎖定同一交談群組中的訊息。  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Broker.BrokerService> 物件代表 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 服務，也就是交談的可定址端點。 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 訊息會從某個服務傳送至另一個服務。 服務會指定要保存訊息的佇列，並指定哪個服務可做為目標的合約。  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Broker.RemoteServiceBinding> 物件代表 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 在與遠端服務進行通訊時，用於安全性與驗證的設定。  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceRoute> 物件代表 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 路由，其中包含服務的位置資訊以及所定義的資料庫。 訊息傳遞需要路由。 根據預設，每個資料庫包含的路由都會將位置指定為目前的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.SqlServer.Management.Smo.Broker>   
 [SQL Server Service Broker](../../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
