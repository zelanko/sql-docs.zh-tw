---
title: SQL Server 管理物件 (SMO) 程式設計指南 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SMO [SQL Server]
- SQL Server Management Objects
- programming [SMO]
ms.assetid: 4cde2b85-2a31-4cac-8d16-7a4196066193
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2381d3485b2c6d2ad2d21ef1e71a4bdf99a34e8f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092799"
---
# <a name="sql-server-management-objects-smo-programming-guide"></a>SQL Server 管理物件 (SMO) 程式設計指南
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件 (SMO) 是針對程式設計管理的所有層面所設計的物件的集合[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Management Objects (RMO) 是封裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫管理的物件集合。  
  
|主題|描述|  
|-----------|-----------------|
|[SMO 使用者入門](getting-started-in-smo.md)|提供如何開始開發 SMO 應用程式的相關資訊
|[建立 SMO 程式](../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)<br /><br /> [程式設計特有的工作](../../relational-databases/server-management-objects-smo/tasks/programming-specific-tasks.md)|提供有關在 Microsoft.SqlServer.management、Microsoft.SqlServer.Management.NotificationServices、Microsoft.SqlServer.Management.Smo、Microsoft.SqlServer.Management.Smo.Agent、Microsoft.SqlServer.Management.Smo.Broker、Microsoft.SqlServer.Management.Smo.Mail、Microsoft.SqlServer.Management.Smo.RegisteredServers、Microsoft.SqlServer.Management.Smo.Wmi 和 Microsoft.SqlServer.Management.Trace 命名空間中，進行 SMO 物件程式開發的詳細資訊。<br /><br /> 這包含撰寫程式以定義資料庫和管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指示。 您可以使用 SMO 來建立資料庫、執行備份、建立作業、設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、指派權限以及執行許多其他的管理工作。|  
|[複寫開發人員文件](../../relational-databases/replication/concepts/replication-developer-documentation.md)|提供有關在 Microsoft.SqlServer.Replication 命名空間中進行 RMO 物件程式開發的詳細資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫開發人員文件](../../relational-databases/replication/concepts/replication-developer-documentation.md)  
  
  
