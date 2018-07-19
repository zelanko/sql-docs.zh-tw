---
title: 安全性稽核事件類別目錄 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [SQL Server], Security Audit event category
- SQL Server event classes, Security Audit event category
ms.assetid: e64f7695-2f23-4adb-b83d-52f147cc1a2f
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1a5af79e427ec6f996a2edb13f79ce067b8a73f3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193288"
---
# <a name="security-audit-event-category-sql-server-profiler"></a>Security Audit 事件類別目錄 (SQL Server Profiler)
  **安全性稽核** 事件類別目錄包含安全性稽核事件。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[Audit Add DB User 事件類別](audit-add-db-user-event-class.md)|表示已當做資料庫使用者在資料庫中加入或移除登入。|  
|[Audit Add Login to Server Role 事件類別](audit-add-login-to-server-role-event-class.md)|表示已在固定伺服器角色中加入或移除登入。|  
|[Audit Add Member to DB Role 事件類別](audit-add-member-to-db-role-event-class.md)|表示已在角色中加入或移除登入。|  
|[Audit Add Role 事件類別](audit-add-role-event-class.md)|表示已在資料庫中加入或移除資料庫角色。|  
|[Audit Addlogin 事件類別](audit-addlogin-event-class.md)|表示已加入或移除登入。|  
|[Audit App Role Change Password 事件類別](audit-app-role-change-password-event-class.md)|表示已變更應用程式角色的密碼。|  
|[Audit Backup 和 Restore 事件類別](audit-backup-and-restore-event-class.md)|表示已發出備份或還原陳述式。|  
|[Audit Broker 交談事件類別](broker-conversation-event-class.md)|報告 Service Broker 對話安全性的相關稽核訊息。|  
|[Audit Broker 登入事件類別](audit-broker-login-event-class.md)|報告 Service Broker 傳輸安全性的相關稽核訊息。|  
|[Audit Change Audit 事件類別](audit-change-audit-event-class.md)|表示已進行稽核追蹤修改。|  
|[Audit Change Database Owner 事件類別](audit-change-database-owner-event-class.md)|表示已檢查變更資料庫擁有者的權限。|  
|[Audit Database Management 事件類別](audit-database-management-event-class.md)|表示已建立、改變或卸除資料庫。|  
|[Audit Database Mirroring Login 事件類別](audit-database-mirroring-login-event-class.md)|報告資料庫鏡像傳輸安全性的相關稽核訊息。|  
|[稽核資料庫物件存取事件類別](audit-database-object-access-event-class.md)|表示已存取資料庫物件，例如結構描述。|  
|[Audit Database Object GDR 事件類別](audit-database-object-gdr-event-class.md)|表示已發生資料庫物件的 GDR 事件。|  
|[Audit Database Object Management 事件類別](audit-database-object-management-event-class.md)|表示已在資料庫物件上執行 CREATE、ALTER 或 DROP 陳述式。|  
|[Audit Database Object Take Ownership 事件類別](audit-database-object-take-ownership-event-class.md)|表示已在資料庫範圍內變更物件的擁有者。|  
|[Audit Database Operation 事件類別](audit-database-operation-event-class.md)|表示已發生各種作業，例如檢查點或訂閱查詢通知。|  
|[Audit Database Principal Impersonation 事件類別](audit-database-principal-impersonation-event-class.md)|表示已在資料庫範圍內發生模擬。|  
|[Audit Database Principal Management 事件類別](audit-database-principal-management-event-class.md)|表示已在資料庫中建立、改變或卸除主體。|  
|[Audit Database Scope GDR 事件類別](audit-database-scope-gdr-event-class.md)|表示使用者已在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中發出陳述式權限的 GRANT、REVOKE 或 DENY。|  
|[稽核 DBCC 事件類別](audit-dbcc-event-class.md)|表示已發出 DBCC 命令。|  
|[稽核全文檢索事件類別](audit-fulltext-event-class.md)|指出發生全文檢索事件。|  
|[Audit Login Change Password 事件類別](audit-login-change-password-event-class.md)|表示使用者已變更其 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入密碼。|  
|[Audit Login Change Property 事件類別](audit-login-change-property-event-class.md)|表示已使用 **sp_defaultdb**、 **sp_defaultlanguage**或 ALTER LOGIN 來修改登入的屬性。|  
|[Audit Login 事件類別](audit-login-event-class.md)|表示使用者已成功登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|[Audit Login Failed 事件類別](audit-login-failed-event-class.md)|表示使用者已嘗試登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 但失敗。|  
|[Audit Login GDR 事件類別](audit-login-gdr-event-class.md)|表示已加入或移除 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入權限。|  
|[Audit Logout 事件類別](audit-logout-event-class.md)|表示使用者已登出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|[Audit Object Derived Permission 事件類別](audit-object-derived-permission-event-class.md)|表示已發出物件的 CREATE、ALTER 或 DROP。|  
|[Audit Schema Object Access 事件類別](audit-schema-object-access-event-class.md)|表示已使用物件權限 (例如 SELECT)。|  
|[Audit Schema Object GDR 事件類別](audit-schema-object-gdr-event-class.md)|表示使用者已在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中發出結構描述物件權限的 GRANT、REVOKE 或 DENY。|  
|[Audit Schema Object Management 事件類別](audit-schema-object-management-event-class.md)|表示已建立、改變或卸除伺服器物件。|  
|[Audit Schema Object Take Ownership 事件類別](audit-schema-object-take-ownership-event-class.md)|表示已檢查變更結構描述物件擁有者的權限。|  
|[Audit Server Alter Trace 事件類別](audit-server-alter-trace-event-class.md)|表示已檢查 ALTER TRACE 權限。|  
|[Audit Server Object GDR 事件類別](audit-server-object-gdr-event-class.md)|表示已發生結構描述物件的 GDR 事件。|  
|[Audit Server Object Management 事件類別](audit-server-object-management-event-class.md)|表示已發生伺服器物件的 CREATE、ALTER 或 DROP 事件。|  
|[Audit Server Object Take Ownership 事件類別](audit-server-object-take-ownership-event-class.md)|表示已變更伺服器物件擁有者。|  
|[Audit Server Operation 事件類別](audit-server-operation-event-class.md)|表示已在伺服器中發生稽核作業。|  
|[Audit Server Principal Impersonation 事件類別](audit-server-principal-impersonation-event-class.md)|表示已在伺服器範圍內發生模擬。|  
|[Audit Server Principal Management 事件類別](audit-server-principal-management-event-class.md)|表示已發生伺服器主體的 CREATE、ALTER 或 DROP。|  
|[Audit Server Scope GDR 事件類別](audit-server-scope-gdr-event-class.md)|表示已發生伺服器權限的 GDR 事件。|  
|[Audit Server Starts and Stops 事件類別](audit-server-starts-and-stops-event-class.md)|表示已修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務狀態。|  
|[Audit Statement Permission 事件類別](audit-statement-permission-event-class.md)|表示已使用陳述式權限。|  
  
## <a name="related-content"></a>相關內容  
 [擴充事件](../extended-events/extended-events.md)  
  
  
