---
title: "SMO 物件模型 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], object model
- SQL Server Management Objects, object model
ms.assetid: bd6e59b6-ca46-42c0-adb2-c9d64cf6e00b
caps.latest.revision: "30"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3b6cce76b87a3adaf31dea029b521fbef5cdb37d
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2018
---
# <a name="smo-object-model"></a>SMO 物件模型
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO 物件模型是由物件階層所組成。 <xref:Microsoft.SqlServer.Management.Smo.Server> 物件是最上層的物件，而所有執行個體類別物件則位於 <xref:Microsoft.SqlServer.Management.Smo.Server> 物件之下。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 類別是包含個別物件階層的最上層類別。 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer>物件代表[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務和網路設定可透過 WMI 提供者。  
  
 除了 <xref:Microsoft.SqlServer.Management.Smo.Server> 和 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 物件之外，還有數個代表工作或或運算的數個公用程式類別，例如 <xref:Microsoft.SqlServer.Management.Smo.Transfer>、<xref:Microsoft.SqlServer.Management.Smo.Backup> 或 <xref:Microsoft.SqlServer.Management.Smo.Restore>  
  
 SMO 物件模型是由數個命名空間所組成。 如需詳細資訊，請參閱 [SMO 命名空間](../../relational-databases/server-management-objects-smo/smo-object-model-namespaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SMO 物件模型圖表](../../relational-databases/server-management-objects-smo/smo-object-model-diagram.md)   
 [SMO 命名空間](../../relational-databases/server-management-objects-smo/smo-object-model-namespaces.md)   
 [組態管理的 WMI 提供者概念](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  
