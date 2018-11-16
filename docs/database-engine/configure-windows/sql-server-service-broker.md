---
title: SQL Server Service Broker | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.SSBMSGTYPEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBCONTRACTPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBQUEUEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBREMSVCBINDPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBROUTEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBPRIORITYPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBSERVICEPROPERTIES.GENERAL.F1
helpviewer_keywords:
- Broker See Service Broker
- SQL Server Service Broker
- Service Broker
ms.assetid: 8b8b3b57-fd46-44de-9a4e-e3a8e3999c1e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 599905aad2a6c6959f4e1e751640533c2d24011a
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51601988"
---
# <a name="sql-server-service-broker"></a>SQL Server Service Broker
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSB](../../includes/sssb-md.md)] 提供在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 這讓開發人員更容易建立使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 元件在不同資料庫間進行通訊的複雜應用程式。 開發人員可以使用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 輕鬆地建立可靠的分散式應用程式。  
  
 使用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的應用程式開發人員不需要撰寫複雜的通訊和傳訊間隔程式，即可將資料工作負載分散在多個資料庫。 這可減少開發和測試工作，因為 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會處理交談內容中的通訊路徑。 此外，還可提升效能。 例如，支援網站的前端資料庫可記錄資訊，並將具有大量處理序的工作傳送到後端資料庫的佇列中。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 可確保所有工作都在交易內容中管理，以確保可靠性和技術一致性。  
  
## <a name="where-is-the-documentation-for-service-broker"></a>Service Broker 的文件集在哪裡？  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的參考文件集包含在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 文件集內。 此參考文件集包含下列章節：  
  
-   [資料定義語言 &#40;DDL&#41; 陳述式 &#40;Transact-SQL&#41;](~/mdx/mdx-data-definition-statements-mdx.md)，適用 CREATE、ALTER 和 DROP 陳述式  
  
-   [Service Broker 陳述式](../../t-sql/statements/service-broker-statements.md)  
  
-   [Service Broker 目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)  
  
-   [Service Broker 相關的動態管理檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
-   [ssbdiagnose 公用程式 &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
 請參閱＜ [舊版文件集](https://go.microsoft.com/fwlink/?LinkId=231312) ＞，了解 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 概念及開發和管理工作。 此文件集未在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 文件集中重製，因為 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 中只有少數 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的變更。  
  
## <a name="whats-new-in-service-broker"></a>Service Broker 的新功能  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]並無導入重大變更。  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中導入了下列變更。  

### <a name="service-broker-and-azure-sql-database-managed-instance"></a>服務代理程式與 Azure SQL Database 受控執行個體

- 不支援跨執行個體服務代理程式 
 - `sys.routes` - 必要條件：從 sys.routes 選取位址。 位址在每個路由上都必須是 LOCAL。 請參閱 [sys.routes](../../relational-databases/system-catalog-views/sys-routes-transact-sql.md)。
 - `CREATE ROUTE` - 您無法使用 `CREATE ROUTE` 來搭配 `LOCAL` 以外的 `ADDRESS`。 請參閱 [CREATE ROUTE](https://docs.microsoft.com/sql/t-sql/statements/create-route-transact-sql)。
 - `ALTER ROUTE` 無法使用 `ALTER ROUTE` 來搭配 `LOCAL` 以外的 `ADDRESS`。 請參閱 [ALTER ROUTE](../../t-sql/statements/alter-route-transact-sql.md)。  
  
### <a name="messages-can-be-sent-to-multiple-target-services-multicast"></a>訊息可以傳送至多個目標服務 (多點傳送)  
 [SEND &#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md) 陳述式的語法已延伸，可透過支援多個交談控制代碼進行多點傳送。  
  
### <a name="queues-expose-the-message-enqueued-time"></a>佇列會公開訊息加入佇列的時間  
 佇列包含一個新的資料行 **message_enqueue_time**，其中顯示訊息已在佇列中的時間。  
  
### <a name="poison-message-handling-can-be-disabled"></a>有害訊息處理可以停用  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md) 和 [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md) 陳述式現在能夠藉由加入子句 `POISON_MESSAGE_HANDLING (STATUS = ON | OFF)` 的方式啟用或停用有害訊息處理。 目錄檢視 **sys.service_queues** 現在包含 **is_poison_message_handling_enabled** 資料行，用來指出有害訊息為啟用或停用狀態。  
  
### <a name="always-on-support-in-service-broker"></a>Service Broker 中的 AlwaysOn 支援  
 如需詳細資訊，請參閱 [Service Broker 與 AlwaysOn 可用性群組 (SQL Server)](../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md)。  
  
  

