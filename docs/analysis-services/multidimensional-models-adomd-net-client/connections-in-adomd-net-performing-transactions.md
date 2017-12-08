---
title: "在 ADOMD.NET 中執行交易 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- transactions [ADOMD.NET]
- ADOMD.NET, transactions
- AdomdTransaction object
ms.assetid: 7978c28b-c255-43c0-ad05-f38604d4d8fe
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5c78445de3ed3b17805bc458ce6078e0d9587eed
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="connections-in-adomdnet---performing-transactions"></a>Connections in ADOMD.NET-執行交易
  在 ADO.NET 中，請使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 物件來管理指定之 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件的交易內容。 這個功能可讓您在相同的內容中執行數個命令。 每個命令都將讀取相同的資料，已讀取的資料不會在每個命令的執行之間變更。  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>類別是實作**System.Data.IDbTransaction**介面，一部分[!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework 類別庫和所有.NET Framework 資料提供者支援的都實作交易。  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 物件只支援讀取認可交易，在這個交易中，會在讀取資料時保持共用鎖定，以避免中途讀取 (Dirty Read)。  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 是用以啟動交易。 為了使用交易，接著會針對啟動交易的連接執行命令。 當您完成交易時，可以回復或認可交易。  
  
## <a name="starting-a-transaction"></a>啟動交易  
 您可以呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> 方法，來建立 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件的執行個體。 下列範例示範如何建立 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 物件的執行個體。  
  
```  
Dim objTransaction As AdomdTransaction = objConnection.BeginTransaction()  
AdomdTransaction objTransaction = objConnection.BeginTransaction();  
```  
  
## <a name="rolling-back-a-transaction"></a>回復交易  
 若要回復現有未完成的交易，可以呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Rollback%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 方法。 如果您在現有完成的交易上呼叫此方法，會擲回例外狀況。  
  
## <a name="committing-a-transaction"></a>認可交易  
 在呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> 方法以啟動交易之後，可以呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Commit%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 方法來完成交易。 如果您在現有完成的交易上呼叫此方法，會擲回例外狀況。  
  
## <a name="see-also"></a>請參閱＜  
 [在 ADOMD.NET 中建立連接](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)   
 [ADOMD.NET 用戶端程式設計](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
