---
title: 使用交易 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eaa6406e04eddbba012cfb61d6ae82a73b7f30bb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "70148676"
---
# <a name="using-transactions"></a>使用交易
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理物件 (SMO) 中，交易處理是藉由使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件，透過與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的連接而達成。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>物件是在建立連接時<xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>由<xref:Microsoft.SqlServer.Management.Smo.Server>物件的屬性所參考。 <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>、<xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> 和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> 之類的方法屬於 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 物件屬性。  
  
## <a name="see-also"></a>另請參閱  
 [建立 SMO 程式](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
