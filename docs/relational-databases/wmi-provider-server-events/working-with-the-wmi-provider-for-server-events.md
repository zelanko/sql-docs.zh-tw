---
title: 使用伺服器事件的 WMI 提供者 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- event notifications [WMI]
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- Service Broker [WMI]
- WMI Provider for Server Events, connection strings
- WMI Provider for Server Events, Service Broker
- notifications [WMI]
- WMI Provider for Server Events, security
ms.assetid: cd974b3b-2309-4a20-b9be-7cfc93fc4389
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 53d14ec8fe32ef665571dde0b7cd4aa4c17c7388
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095489"
---
# <a name="working-with-the-wmi-provider-for-server-events"></a>使用伺服器事件的 WMI 提供者
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  本主題會提供您使用伺服器事件的 WMI 提供者進行程式設計前應該考慮的指導方針。  
  
## <a name="enabling-service-broker"></a>啟用 Service Broker  
 伺服器事件的 WMI 提供者可透過將事件的 WQL 查詢轉譯為目標系統中的事件通知來運作。 了解事件通知如何運作在根據提供者進行程式設計時可能很有用。 如需詳細資訊，請參閱＜ [伺服器事件的 WMI 提供者概念](https://technet.microsoft.com/library/ms180560.aspx)＞。  
  
 特別是，WMI 提供者所建立的事件通知使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來傳送伺服器事件的相關訊息，因此必須在產生事件的每個地方啟用此服務。 如果您的程式查詢伺服器執行個體上的事件，必須啟用該執行個體之 msdb 中的 [!INCLUDE[ssSB](../../includes/sssb-md.md)]，因為那是提供者所建立之目標 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 服務 (名稱為 SQL/Notifications/ProcessWMIEventProviderNotification/v1.0) 的位置。 如果您的程式查詢資料庫中或特定資料庫物件上的事件，則必須在該目標資料庫中啟用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 。 如果部署應用程式之後沒有啟用對應的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ，基礎事件通知所產生的任何事件都會傳送到事件通知所使用的服務佇列，但是不會傳回到您的 WMI 管理應用程式，直到啟用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 為止。  
  
 下列查詢會判斷伺服器執行個體上啟用的 Service Broker，以及 Broker 執行個體 GUID：  
  
```  
SELECT name, is_broker_enabled, service_broker_guid FROM sys.databases;  
```  
  
 msdb 的 Service Broker GUID 特別需要注意，因為那是提供者目標服務的位置。  
  
 若要在資料庫中啟用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ，使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式的 ENABLE_BROKER SET 選項。  
  
## <a name="specifying-a-connection-string"></a>指定連接字串  
 應用程式會藉由連接到伺服器事件的 WMI 提供者所定義的 WMI 命名空間，將該提供者導向至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 Windows WMI 服務會將此命名空間對應至提供者 DLL (Sqlwep.dll,) 並將其載入至記憶體。 每個執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有它自己的 WMI 命名空間，預設為： \\ \\。\\*根*\Microsoft\SqlServer\ServerEvents\\*instance_name*。 *instance_name*中的預設安裝的預設值為 MSSQLSERVER [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="permissions-and-server-authentication"></a>權限和伺服器驗證  
 若要存取伺服器事件的 WMI 提供者，WMI 管理應用程式起始的用戶端在應用程式之應用程式連接字串指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中，必須對應到 Windows 驗證的登入或群組。  
  
## <a name="permissions-and-event-notification-scope"></a>權限和事件通知範圍  
 伺服器事件的 WMI 提供者會將 WQL 查詢轉譯為目標資料庫中的事件通知。 因為這個緣故，呼叫應用程式不但必須擁有存取提供者所需的最小權限，也必須擁有資料庫的正確權限，才能建立所需的事件通知。 以下是權限：  
  
-   若要建立以資料庫為範圍的事件通知，至少需要目前資料庫的 CREATE DATABASE DDL EVENT NOTIFICATION 權限。  
  
-   若要建立以伺服器為範圍之 DDL 陳述式的事件通知，至少需要伺服器的 CREATE DDL EVENT NOTIFICATION 權限。  
  
-   若要建立追蹤事件的事件通知，至少需要伺服器的 CREATE TRACE EVENT NOTIFICATION 權限。  
  
-   若要建立以佇列為範圍的事件通知，至少需要佇列的 ALTER 權限。  
  
 如需有關 WQL 查詢範圍的詳細資訊，請參閱＜ [搭配伺服器事件的 WMI 提供者使用 WQL](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)＞。  
  
 為說明範圍，請考慮使用包含下列 WQL 查詢的 WMI 提供者應用程式：  
  
```  
SELECT * FROM ALTER_TABLE  
WHERE DatabaseName = "AdventureWorks2012"   
    AND SchemaName = "Person"  
    AND ObjectName = "Person"  
    AND ObjectType = "TABLE";  
```  
  
 WMI 提供者會將此查詢轉譯為 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中建立的事件通知。 也就是說，呼叫端必須具備所需的權限，才能建立此種事件通知，特別是 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的 CREATE DATABASE DDL EVENT NOTIFICATION 權限。  
  
 如果 WQL 查詢指定伺服器層級範圍的事件通知 (例如，透過發出查詢 SELECT * FROM ALTER_TABLE)，呼叫應用程式必須具備伺服器層級的 CREATE DDL EVENT NOTIFICATION 權限。 請注意，伺服器範圍的事件通知會儲存在 master 資料庫中。 您可以使用 [sys.server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md) 目錄檢視來查看其中繼資料。  
  
> [!NOTE]  
>  WMI 提供者所建立的事件通知範圍 (伺服器、資料庫或物件) 最終取決於 WMI 提供者所使用之權限驗證處理的結果。 這會受到呼叫提供者之使用者的權限集，以及要查詢之資料庫的驗證之影響。  
>   
>  在上述範例中，提供者會先嘗試建立資料庫範圍的事件通知 (`ON DATABASE`)。 如果提供者確認資料庫存在，而且呼叫端具有在其上建立事件通知所需的權限，註冊作業就會成功， 如果不成功，提供者會嘗試在伺服器上建立事件通知 (`ON SERVER`)。 假設這個嘗試成功，發生在伺服器上的所有 `ALTER_TABLE` 事件都會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序傳送到 WMI 服務處理序。 不過，提供者會篩選出沒有套用到 `AdventureWorks` 資料庫的任何事件。 雖然此處理可能會增加事件範圍所需的網路流量，但是也可讓您擁有在建立 WQL 查詢前，於資料庫上註冊這些查詢的彈性，然後在建立資料庫之後接收事件資料，就可以在其上啟動 DDL 活動。  
  
## <a name="permissions-and-message-verification"></a>權限和訊息驗證  
 如果下列兩個條件同時成立，WMI 提供者不會傳送事件通知的訊息：  
  
-   透過 WMI 提供者建立事件通知的使用者不再存在於資料庫中，或者不再具備建立類似事件通知所需的權限。  
  
-   在下列事件上會建立事件通知：  
  
    -   DROP_LOGIN  
  
    -   ALTER_LOGIN  
  
    -   DROP_USER  
  
    -   ALTER_USER  
  
    -   ADD_ROLE_MEMBER  
  
    -   DROP_ROLE_MEMBER  
  
    -   ADD_SERVER_ROLE_MEMBER  
  
    -   DROP_SERVER_ROLE_MEMBER  
  
    -   DENY 或 REVOKE (僅適用於 ALTER DATABASE、ALTER ANY DATABASE EVENT NOTIFICATION、CREATE DATABASE DDL EVENT NOTIFICATION、CONTROL SERVER、ALTER ANY EVENT NOTIFICATION、CREATE DDL EVENT NOTIFICATION 或 CREATE TRACE EVENT NOTIFICATION 權限)。  
  
## <a name="working-with-event-data-on-the-client-side"></a>使用用戶端上的事件資料  
 WMI 提供者伺服器事件會在目標資料庫中，建立所需的事件通知事件通知事件會將資料傳送至目標服務名稱為的 msdb 中**SQL/通知/ProcessWMIEventProviderNotification/v1.0**。 目標服務會將事件放入 **msdb** 中，名稱為 **WMIEventProviderNotificationQueue**的佇列 (服務和佇列會以動態方式提供者建立第一次連接到時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。)提供者然後會從此佇列讀取 XML 事件資料，並將它轉換成受管理的物件格式 (MOF) 中，然後再回到用戶端應用程式。 MOF 資料是由 WQL 查詢所要求的事件屬性所組成，做為通用訊息模型 (CIM) 類別定義。 每個屬性都有一個對應的 CIM 類型。 例如，`SPID`屬性會傳回當做 CIM 類型**Sint32**。 每個屬性的 CIM 類型都會列在＜ [伺服器事件類別和屬性的 WMI 提供者](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md)＞中的每個事件類別之下。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器事件的 WMI 提供者概念](https://technet.microsoft.com/library/ms180560.aspx)  
  
  
