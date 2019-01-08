---
title: 了解伺服器事件的 WMI 提供者 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- architecture [WMI]
- SQL Server Agent [WMI]
- WMI Provider for Server Events, about WMI Provider for Server Events
ms.assetid: 8fd7bd18-76d0-4b28-8fee-8ad861441ab2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2deedb64e5c8995524978a19b02110a068bde08d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358210"
---
# <a name="understanding-the-wmi-provider-for-server-events"></a>了解伺服器事件的 WMI 提供者
  WMI Provider for Server Events 可讓您使用 Windows Management Instrumentation (WMI) 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中監視事件。 提供者的運作方式是將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 轉換成 Managed WMI 物件。 使用這個提供者的 WMI 可利用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中產生事件通知的任何事件。 另外，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 是與 WMI 互動的管理應用程式，所以它可回應這些事件，方法是增加 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在舊版本上所涵蓋的事件範圍。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 之類的管理應用程式可藉由發出 WMI 查詢語言 (WQL) 陳述式，使用伺服器事件的 WMI 提供者來存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 WQL 是結構化查詢語言 (SQL) 的簡化子集，具有一些 WMI 特定的延伸模組。 在使用 WQL 時，應用程式會針對特定的資料庫或資料庫物件來擷取事件類型。 伺服器事件的 WMI 提供者會將查詢轉譯為事件通知，以便在目標資料庫中有效地建立事件通知。 如需有關事件通知中的運作方式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱 < [WMI 提供者伺服器事件概念](https://technet.microsoft.com/library/ms180560.aspx)。 可查詢的事件會列在[伺服器事件類別和屬性的 WMI 提供者](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md)。  
  
 事件發生時觸發事件通知，傳送訊息，訊息中的預先定義的目標服務會進入**msdb**命名為**SQL/Notifications/ProcessWMIEventProviderNotification/v1.0**. 服務會將事件放在預先定義的佇列**msdb**命名為**WMIEventProviderNotificationQueue**。 (當此服務手冊連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，提供者會同時動態地建立服務和佇列)。接著，提供者會從此佇列讀取事件資料，並將其轉換為 Managed 物件格式 (MOF)，然後再將其傳回到應用程式。 下圖顯示這項程序。  
  
 ![WMI Provider for Server Events 的流程圖](../../../2014/database-engine/dev-guide/media/wmi-provider-functional-spec.gif "WMI Provider for Server Events 的流程圖")  
  
 例如，請考慮使用下列 WQL 查詢：  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS  
WHERE DatabaseName = 'AdventureWorks'  
```  
  
 回應此查詢時，伺服器事件的 WMI 提供者會在目標資料庫中建立相等的事件通知：  
  
```  
USE AdventureWorks ;  
GO  
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9  
    ON DATABASE  
    WITH FAN_IN  
    FOR DDL_DATABASE_LEVEL_EVENTS  
    TO SERVICE  
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0',   
        'A7E5521A-1CA6-4741-865D-826F804E5135';  
GO  
```  
  
 在此範例中，`SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9` 是由前置詞 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 GUID 構成的 `SQLWEP_` 識別碼。 `SQLWEP` 會為每個識別碼建立一個新的 GUID。 該值`A7E5521A-1CA6-4741-865D-826F804E5135`中`TO SERVICE`子句會識別中的 broker 執行個體的 GUID **msdb**資料庫。  
  
 如需如何使用 WQL 的詳細資訊，請參閱[搭配伺服器事件的 WMI 提供者使用 WQL](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)。  
  
 管理應用程式會藉由連接到提供者所定義的 WMI 命名空間，將該伺服器事件的 WMI 提供者導向至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 Windows WMI 服務會將此命名空間對應至提供者 DLL (Sqlwep.dll,) 並將其載入至記憶體。 提供者管理伺服器事件的 WMI 命名空間，每個執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而且格式為： \\ \\。\\*根*\Microsoft\SqlServer\ServerEvents\\*instance_name*，其中*instance_name*預設為 MSSQLSERVER。 如需有關如何連接到的執行個體的 WMI 命名空間[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 搭配伺服器事件的 WMI 提供者使用 WQL](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)。  
  
 不管伺服器上有多少 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，都只會將提供者 DLL (Sqlwep.dll) 載入到伺服器作業系統的 WMI 主機服務一次。  
  
 如需[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式管理應用程式使用伺服器事件的 WMI 提供者，請參閱[範例：建立 SQL Server Agent 警示使用 WMI Provider for Server Events](https://technet.microsoft.com/library/ms186385.aspx)。 如需在 managed 程式碼中使用伺服器事件的 WMI 提供者的管理應用程式的範例，請參閱[範例：使用 WMI 事件提供者，在 Managed 程式碼](https://technet.microsoft.com/library/ms179315.aspx)。 也會提供有關 WMI 中詳細的資訊[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器事件的 WMI 提供者概念](https://technet.microsoft.com/library/ms180560.aspx)  
  
  
