---
title: Common Language Runtime (CLR) 整合程式設計概念 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- CLR [SQL Server] See common language runtime [SQL Server]
- Database Engine [SQL Server], .NET Framework
- .NET Framework [SQL Server], Database Engine programming
- common language runtime [SQL Server]
- .NET Framework [SQL Server]
ms.assetid: 951bf851-3e6e-4361-ae6a-2bcd5b837ebd
caps.latest.revision: 56
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b4b2ee2815f89770d3c9af182237fb7d888424bc
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350090"
---
# <a name="common-language-runtime-clr-integration-programming-concepts"></a>Common Language Runtime (CLR) 整合程式設計概念
  從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 開始，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 具備 .NET Framework for [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 的 Common Language Runtime (CLR) 元件整合功能。 這表示您現在可以使用任何 .NET Framework 語言 (包括 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET 及 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#)，撰寫預存程序、觸發程序、使用者定義型別、使用者定義函數、使用者定義彙總及資料流資料表值函數。  
  
 Microsoft.SqlServer.Server 命名空間在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中包含用於 CLR 程式設計的核心功能。 不過，Microsoft.SqlServer.Server 命名空間會記載在 .NET Framework SDK 中。 此文件不包含在《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中。  
  
> [!IMPORTANT]  
>  根據預設，.NET Framework 會與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一起安裝，但是 .NET Framework SDK 則不會。 如果 SDK 未安裝在電腦上，也不包含在線上叢書集合中，本節中的 SDK 內容連結將不會有任何作用。 請安裝 .NET Framework SDK。 安裝之後，將 SDK 加入至線上叢書集合和目錄中的指示[安裝.NET Framework SDK](http://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)。  
  
 下表列出本節的主題。  
  
 [通用語言執行平台&#40;CLR&#41;整合概觀](common-language-runtime-integration-overview.md)  
 提供 CLR 的簡短概觀，並描述在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中使用此技術的方法和原因。 描述使用 CLR 建立資料庫物件的優點。  
  
 [組件 &#40;Database Engine&#41](assemblies-database-engine.md)  
 描述如何使用組件在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中部署以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework Common Language Runtime (CLR) 主控的其中一種 Managed 程式碼語言 (非 [!INCLUDE[tsql](../../../includes/tsql-md.md)]) 所編寫的函數、預存程序、觸發程序、使用者定義彙總，以及使用者定義型別。  
  
 [建立資料庫物件與 Common Language Runtime &#40;CLR&#41;整合](database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)  
 描述可以使用 CLR 建立的物件種類，並檢閱建立 CLR 資料庫物件的需求。  
  
 [從 CLR 資料庫物件進行資料存取](data-access/data-access-from-clr-database-objects.md)  
 描述 CLR 常式如何存取儲存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體中的資料。  
  
 [CLR 整合安全性](security/clr-integration-security.md)  
 描述 CLR 整合的安全性模型。  
  
 [偵錯 CLR 資料庫物件](debugging-clr-database-objects.md)  
 描述為 CLR 資料庫物件偵錯的限制和需求。  
  
 [部署 CLR 資料庫物件](deploying-clr-database-objects.md)  
 描述如何將組件部署至實際伺服器。  
  
 [管理 CLR 整合組件](assemblies/managing-clr-integration-assemblies.md)  
 描述如何建立和卸除 CLR 整合組件。  
  
 [監視與疑難排解受管理的資料庫物件](monitoring-and-troubleshooting-managed-database-objects.md)  
 提供可用於監視和疑難排解 Managed 資料庫物件以及在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中執行之組件的工具相關資訊。  
  
 [通用語言執行平台 &#40;CLR&#41; 整合的使用案例和範例](../../database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
 描述使用 CLR 物件的使用狀況和程式碼範例。  
  
## <a name="see-also"></a>另請參閱  
 [組件&#40;Database Engine&#41;](assemblies-database-engine.md)   
 [安裝.NET Framework SDK](http://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)  
  
  
