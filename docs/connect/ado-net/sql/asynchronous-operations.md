---
title: 非同步作業
description: 說明如何使用在 .NET Framework 所用非同步模型之後建立模型的 API，來執行非同步資料庫作業。
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: bc2a921e3aec0068c11b2baab45c396d853a1a36
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897058"
---
# <a name="asynchronous-operations"></a>非同步作業

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

某些資料庫作業 (例如命令執行) 可能需要大量時間才能完成。 在這種情況下，單一執行緒的應用程式必須封鎖其他作業並等候命令完成，才會繼續它們自己的作業。 相反地，能夠將長時間執行的作業指定給背景執行緒，即允許前景執行緒在整個作業期間保持使用中。 例如，在 Windows 應用程式中，將長時間執行的作業委派給背景執行緒，可讓使用者介面執行緒在作業執行時維持回應。  
  
.NET 提供了數個標準的非同步設計模式，讓開發人員可用來利用背景執行緒，並釋放使用者介面或高優先順序的執行緒，以便在其 <xref:Microsoft.Data.SqlClient.SqlCommand> 類別中完成其他作業。 具體而言，<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 和 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 方法 (與 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> 和 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A> 方法配對) 都提供非同步支援。  
  
> [!NOTE]
>  非同步程式設計是 .NET 的一個核心功能。 如需開發人員可使用之各種非同步技術的詳細資訊，請參閱[以非同步的方式呼叫同步方法](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously) \(部分機器翻譯\)。  
  
雖然使用具有 ADO.NET 功能的非同步技術並不會新增任何特殊考量，但請務必留意建立多執行緒應用程式的優點和陷阱。 此節中後續的範例會指出在建置包含多執行緒功能的應用程式時，開發人員必須考慮的數個重要問題。  
  
## <a name="in-this-section"></a>本節內容  
[使用回撥的 Windows 應用程式](windows-applications-callbacks.md)  
提供範例來示範如何安全地執行非同步命令，並正確處理與表單及其來自不同執行緒的內容互動。  
  
[使用 Wait 控制代碼的 ASP.NET 應用程式](aspnet-apps-use-wait-handles.md)  
提供範例來示範如何從 ASP.NET 網頁執行多個並行命令，並使用 Wait 控制代碼來管理完成所有命令的作業。  
  
[在主控台應用程式中輪詢](poll-console-applications.md)  
提供範例來示範如何使用輪詢，以等待主控台應用程式的非同步命令執行完成。 此技術在類別庫或其他沒有使用者介面的應用程式中也有效。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
- [以非同步的方式呼叫同步方法](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously) \(部分機器翻譯\)
