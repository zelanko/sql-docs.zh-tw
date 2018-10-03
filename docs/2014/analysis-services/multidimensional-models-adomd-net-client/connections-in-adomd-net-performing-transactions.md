---
title: 在 ADOMD.NET 中執行交易 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- transactions [ADOMD.NET]
- ADOMD.NET, transactions
- AdomdTransaction object
ms.assetid: 7978c28b-c255-43c0-ad05-f38604d4d8fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aa3fd6ad27ced739c6d8ebd5d2fb2ad00bd6f707
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169748"
---
# <a name="performing-transactions-in-adomdnet"></a>在 ADOMD.NET 中執行交易
  在 ADO.NET 中，請使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 物件來管理指定之 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件的交易內容。 這個功能可讓您在相同的內容中執行數個命令。 每個命令都將讀取相同的資料，已讀取的資料不會在每個命令的執行之間變更。  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 類別是 `System.Data.IDbTransaction` 介面的實作，屬於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 類別庫的一部分，會由支援交易的所有 .NET Framework 資料提供者實作。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [在 ADOMD.NET 中建立連接](connections-in-adomd-net.md)   
 [ADOMD.NET 用戶端程式設計](adomd-net-client-programming.md)  
  
  
