---
title: "使用交易 |Microsoft 文件"
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
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
caps.latest.revision: "37"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 556763c88080025e967b7e85b48f5579d2eebcb8
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2018
---
# <a name="using-transactions"></a>使用交易
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理物件 (SMO) 中，交易處理是藉由使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件，透過與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的連接而達成。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>所參考物件<xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>屬性<xref:Microsoft.SqlServer.Management.Smo.Server>物件在建立連線時。 <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>、<xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> 和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> 之類的方法屬於 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 物件屬性。  
  
## <a name="see-also"></a>另請參閱  
 [建立 SMO 程式](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
