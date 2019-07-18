---
title: SMO 命名空間 |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], namespaces
- namespaces [SMO]
- SQL Server Management Objects, namespaces
ms.assetid: 7bfabe4d-9f4c-4bc9-b998-93bd2b50ee8a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7e3787429a4652e1893f56e0a8a4f33d9e72ba84
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097958"
---
# <a name="smo-object-model-namespaces"></a>SMO 物件模型命名空間
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件 (SMO) 具有多種命名空間。 不同的命名空間代表 SMO 內不同的功能區域。  
  
 在  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，SMO 組件位於 C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies\ 資料夾中。  
  
## <a name="namespaces"></a>命名空間  
 SMO 命名空間有：  
  
|類別|函數|  
|-----------|--------------|  
|<xref:Microsoft.SqlServer.Management.Smo>|包含執行個體類別、 公用程式類別和列舉，用來以程式設計方式操作[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|<xref:Microsoft.SqlServer.Management.Common>|包含 Replication Management Objects (RMO) 和 SMO 通用的類別，例如連接類別。|  
|<xref:Microsoft.SqlServer.Management.Smo.Agent>|包含表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的類別。|  
|<xref:Microsoft.SqlServer.Management.Smo.Wmi>|包含表示 WMI 提供者的類別。|  
|<xref:Microsoft.SqlServer.Management.Smo.RegisteredServers>|包含表示已註冊的伺服器的類別。|  
|<xref:Microsoft.SqlServer.Management.Smo.Mail>|包含表示 Database Mail 的類別。|  
|<xref:Microsoft.SqlServer.Management.Smo.Broker>|包含表示 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的類別。|  
  
  
