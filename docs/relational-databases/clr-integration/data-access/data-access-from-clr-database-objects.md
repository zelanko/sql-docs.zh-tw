---
title: 從 CLR 資料庫物件的資料存取 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], data access
- routines [CLR integration]
- data access [CLR integration]
- ADO.NET [CLR integration]
- internal data access [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], data access
- managed code [SQL Server], database objects
- .NET Data Access Provider for SQL Server [CLR integration]
- managed code [SQL Server], data access
- SqlClient provider
- in-process data access providers [CLR integration]
ms.assetid: 9a0f4dee-71c1-42e9-a85e-52382807010f
caps.latest.revision: 41
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1ff4b57fc7557fd2fd339e08b1529605d505cd44
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35701839"
---
# <a name="data-access-from-clr-database-objects"></a>從 CLR 資料庫物件進行資料存取
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Common language runtime (CLR) 常式可以輕鬆存取資料的執行個體中儲存[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體中，以及儲存在遠端執行個體中的資料。 常式可以存取的特定資料取決於藉以執行程式碼的使用者內容。 從 CLR 資料庫物件中的資料存取使用.NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，也稱為**SqlClient**。 這與開發人員從 Managed 用戶端與中間層應用程式存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料所使用的提供者相同。 因為這個緣故，您可以利用 ADO.NET 的知識和**SqlClient**用戶端和中介層應用程式中。  
  
> [!NOTE]  
>  根據預設，執行資料存取不允許使用使用者定義型別方法與使用者定義函數。 您必須設定**DataAccess**屬性**SqlMethodAttribute**或**SqlFunctionAttribute**至**DataAccessKind.Read**啟用從使用者定義型別 (UDT) 方法或使用者定義函式的唯讀資料存取。 資料修改作業無法從 UDT 或使用者定義函數進行，如果嘗試進行，則會在執行階段擲回例外狀況。  
  
 本節僅討論從 CLR 資料庫物件中存取資料時，功能與行為上的特定差異。 如需有關 ADO.NET 功能的詳細資訊，請參閱隨附在 .NET Framework SDK 中的 ADO.NET 文件集。  
  
 下表列出本節的主題。  
  
 [內容連接](../../../relational-databases/clr-integration/data-access/context-connection.md)  
 描述 SQL Server 的內容連接。  
  
 [連接的模擬和認證](../../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
 描述模擬連接以及連接認證。  
  
 [ADO.NET 的 SQL Server 同處理序特定延伸模組](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 討論同處理序特定**SqlPipe**， **SqlContext**， **SqlTriggerContext**，和**SqlDataRecord**物件。  
  
 [CLR 整合和交易](../../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
 描述 System.Transactions 命名空間中提供的新交易架構如何整合 ADO.NET 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 整合。  
  
 [從 CLR 資料庫物件的 XML 序列化](http://msdn.microsoft.com/library/ac84339b-9384-4710-bebc-01607864a344)  
 說明如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中啟用 CLR 資料庫物件的 XML 序列化案例。  
  
  
