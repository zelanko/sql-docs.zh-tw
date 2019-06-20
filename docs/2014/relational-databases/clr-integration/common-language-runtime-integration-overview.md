---
title: Common Language Runtime (CLR) 整合概觀 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- managed code [SQL Server]
- common language runtime [SQL Server], about CLR integration
- cross-language integration
- integrating CLR [SQL Server]
- .NET Framework [SQL Server], common language runtime
- code access security [CLR integration]
- managed code [SQL Server], CLR integration
ms.assetid: 7be9e644-36a2-48fc-9206-faf59fdff4d7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a7764c6e8e45b56e43e592e70b1c85b8d4744b69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919309"
---
# <a name="common-language-runtime-clr-integration-overview"></a>Common Language Runtime (CLR) 整合概觀
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 現在具備 .NET Framework for [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 的 Common Language Runtime (CLR) 元件整合功能。 CLR 提供含有如跨語言整合、程式碼存取安全性、物件存留期間管理，以及偵錯和設定檔作業支援的 Managed 程式碼。 對於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用者和應用程式開發人員，CLR 整合意味著您現在可以使用任何 .NET Framework 語言 (包括 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#) 撰寫預存程序、觸發程序、使用者定義型別、使用者定義函數 (純量和資料表值) 和使用者定義彙總函式。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含預先安裝的 .NET Framework 版本 4。  
  
 這項整合的主要優點包括：  
  
-   **更好的程式設計模型。** .NET Framework 語言在許多方面比 Transact-SQL 豐富，可提供先前未提供給 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 開發人員的建構與功能。 開發人員也可以運用提供一組廣大類別的 .NET Framework 程式庫功能，可用於快速而有效率地解決程式設計問題。  
  
-   **可增進的安全和安全性。** Managed 程式碼會在 Database Engine 主控的 Common Language Run-time 環境下執行。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會運用此環境提供更安全的替代方式給舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 所提供的擴充預存程序。  
  
-   **定義資料類型和彙總函式的能力。** 使用者定義型別和使用者定義彙總是兩個新的 Managed 資料庫物件，它們可以擴充 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的儲存和查詢功能。  
  
-   **透過標準化環境簡化的開發。** [!INCLUDE[msCoName](../../../includes/msconame-md.md)]資料庫開發會整合到後續版本的  Visual Studio .NET 開發環境中。 開發人員用來開發與偵錯資料庫物件和指令碼的工具，與他們用來撰寫中介層或用戶層的 .NET Framework 元件和服務的工具是一樣的。  
  
-   **更佳的效能和延展性的可能性。** 在許多情況下，.NET Framework 語言編譯和執行模型會透過 Transact-SQL 提供改善的效能。  
  
 下表列出本節中的主題。  
  
 [CLR 整合的概觀](clr-integration-overview.md)  
 描述可以使用 CLR 整合建立的物件種類，並檢閱使用 CLR 整合建立資料庫物件的需求。  
  
 [CLR 整合的新功能](clr-integration-what-s-new.md)  
 描述這個版本的新功能。  
  
 [CLR 整合的架構](../../database-engine/dev-guide/architecture-of-clr-integration.md)  
 描述 CLR 整合的設計目標。  
  
 [啟用 CLR 整合](clr-integration-enabling.md)  
 說明如何啟用 CLR 整合。  
  
## <a name="see-also"></a>另請參閱  
 [安裝.NET Framework](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [CLR 整合的效能](clr-integration-architecture-performance.md)  
  
  
