---
title: 非同步作業
description: 說明如何使用在 .NET Framework 所用非同步模型之後建立模型的 API，來執行非同步資料庫作業。
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 79cde936328476408fabb3df7a6bff8d983ace1c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452319"
---
# <a name="asynchronous-operations"></a>非同步作業

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

某些資料庫作業（例如命令執行）可能需要很長的時間才能完成。 在這種情況下，單一執行緒應用程式必須封鎖其他作業並等候命令完成，然後才能繼續執行自己的作業。 相反地，能夠將長時間執行的作業指定給背景執行緒，即允許前景執行緒在整個作業期間保持使用中。 例如，在 Windows 應用程式中，將長時間執行的作業委派給背景執行緒，可讓使用者介面執行緒在作業執行時維持回應。  
  
.NET 提供了數個標準非同步設計模式，開發人員可以使用它來利用背景執行緒，並釋放使用者介面或高優先順序執行緒，以在其 <xref:Microsoft.Data.SqlClient.SqlCommand> 類別中完成其他作業。 具體而言，<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 和 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 方法（與 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> 和 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A> 方法配對）都會提供非同步支援。  
  
> [!NOTE]
>  非同步程式設計是 .NET 的核心功能。 如需開發人員可用之不同非同步技術的詳細資訊，請參閱[以非同步方式呼叫同步方法](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)。  
  
雖然使用具有 ADO.NET 功能的非同步技術並不會加入任何特殊考慮，但請務必留意建立多執行緒應用程式的優點和陷阱。 本章節中的範例會指出在建立包含多執行緒功能的應用程式時，開發人員必須考慮的幾個重要問題。  
  
## <a name="in-this-section"></a>本節內容  
[使用回撥的 Windows 應用程式](windows-applications-callbacks.md)  
提供範例，示範如何安全地執行非同步命令，並正確地處理與表單的互動，以及從不同的執行緒中的內容。  
  
[使用 Wait 控制代碼的 ASP.NET 應用程式](aspnet-apps-use-wait-handles.md)  
提供範例示範如何從 ASP.NET 網頁執行多個並行命令，並使用等候控制碼來管理完成所有命令的作業。  
  
[在主控台應用程式中輪詢](poll-console-applications.md)  
提供範例示範如何使用輪詢，以等待從主控台應用程式完成非同步命令執行。 這項技術在類別庫或其他沒有使用者介面的應用程式中也是有效的。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
- [非同步呼叫同步方法](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)
