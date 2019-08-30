---
title: 程式設計特定工作 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SQL Server Management Objects, tasks
- SMO [SQL Server], programming
- SMO [SQL Server], tasks
ms.assetid: a15949ef-88d9-4205-892e-0b66588b4fcc
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f23b7844bcff234594db87875e89a89f0f073be9
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148401"
---
# <a name="programming-specific-tasks"></a>程式設計特有的工作
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  使用 SMO 物件的程式設計特有工作包含只有具備特定功能之程式所需要的複雜主題，例如，備份、監視統計資料、複寫、管理執行個體物件，以及設定組態選項。  
  
|主題|描述|  
|-----------|-----------------|  
|[在 SMO 中使用連結的伺服器](../../../relational-databases/server-management-objects-smo/tasks/using-linked-servers-in-smo.md)|描述 SMO 如何使用 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 物件連結 OLE-DB 伺服器。|  
|[在 SMO 中設定 SQL Server](../../../relational-databases/server-management-objects-smo/tasks/configuring-sql-server-in-smo.md)|描述如何在 SMO 中檢視與修改 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的組態設定。|  
|[使用資料表和索引資料分割](../../../relational-databases/server-management-objects-smo/tasks/using-table-and-index-partitioning.md)|描述如何在 SMO 中使用索引和資料表資料分割。|  
|[使用檔案群組和檔案來儲存資料](../../../relational-databases/server-management-objects-smo/tasks/using-filegroups-and-files-to-store-data.md)|描述如何在 SMO 中使用檔案群組。|  
|[使用 WMI 提供者管理服務和網路設定](../../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)|描述使用代表組態管理的 WMI 提供者之 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 物件，追蹤 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的數個方式。|  
|[使用資料庫物件](../../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-database-objects.md)|描述如何建立代表 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之物件的執行個體類別。|  
|[管理使用者、角色和登入](../../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)|描述如何在 SMO 中使用安全性角色。|  
|[授與、撤銷和拒絕權限](../../../relational-databases/server-management-objects-smo/tasks/granting-revoking-and-denying-permissions.md)|描述如何使用 SMO 授與、撤銷與拒絕使用者或角色成員的權限。|  
|[使用加密](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)|描述如何在 SMO 中使用加密來保護資料。|  
|[使用 SQL Server Agent 排程自動管理工作](../../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md)|描述如何使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 監視、報告與排程 SMO 中的工作。|  
|[備份和還原資料庫與交易記錄](../../../relational-databases/server-management-objects-smo/tasks/backing-up-and-restoring-databases-and-transaction-logs.md)|描述如何在 SMO 中備份及還原資料庫和交易記錄。|  
|[指令碼](../../../relational-databases/server-management-objects-smo/tasks/scripting.md)|描述如何在 SMO 中撰寫物件的指令碼，並探索物件之間的相依性。|  
|[傳送資料](../../../relational-databases/server-management-objects-smo/tasks/transferring-data.md)|描述如何在 SMO 中傳送資料。|  
|[使用 Database Mail](../../../relational-databases/server-management-objects-smo/tasks/using-database-mail.md)|描述 SMO 如何使用電子郵件服務。|  
|[管理 Service Broker](../../../relational-databases/server-management-objects-smo/tasks/managing-service-broker.md)|描述如何使用 SMO 設定 Service Broker。|  
|[使用 XML 結構描述](../../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md)|描述如何在 SMO 中使用 XML 資料類型。|  
|[使用同義字](../../../relational-databases/server-management-objects-smo/tasks/using-synonyms.md)|描述如何在 SMO 中建立同義字。|  
|[使用訊息](../../../relational-databases/server-management-objects-smo/tasks/using-messages.md)|描述如何使用系統訊息，以及如何定義您自己的使用者定義訊息。|  
|[實作全文檢索搜尋](../../../relational-databases/server-management-objects-smo/tasks/implementing-full-text-search.md)|描述如何在 SMO 中實作全文檢索搜尋目錄與索引。|  
|[實作端點](../../../relational-databases/server-management-objects-smo/tasks/implementing-endpoints.md)|描述如何建立端點來處理資料庫鏡像、SOAP 要求與 Service Broker 的裝載。|  
|[建立和更新統計資料](../../../relational-databases/server-management-objects-smo/tasks/creating-and-updating-statistics.md)|描述如何在 SMO 中設定與監視資料庫上的統計資料。|  
|[追蹤及重新執行事件](../../../relational-databases/server-management-objects-smo/tasks/tracing-and-replaying-events.md)|描述如何在 SMO 中使用**trace**和**replay**物件來追蹤和重新執行事件。|  
  
  
