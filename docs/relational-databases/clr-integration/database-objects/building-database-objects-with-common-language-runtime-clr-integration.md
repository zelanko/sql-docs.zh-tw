---
title: 建立使用 Common Language Runtime (CLR) 整合的資料庫物件 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- database objects [CLR integration], building
- common language runtime [SQL Server], building database objects
- managed code [SQL Server], database objects
- building database objects [CLR integration]
- .NET Framework routines [SQL Server]
ms.assetid: ce34132c-bfa3-447b-9131-b6e17c672efe
caps.latest.revision: 48
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6bd6cbf88b471af8d80f61f65ac0903a740a9675
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37358960"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>利用 Common Language Runtime (CLR) 整合建置資料庫物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以搭配 .NET Framework Common Language Runtime (CLR) 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 整合來建立資料庫物件。 執行內的 managed 程式碼[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]稱為 「 CLR 常式 」。 這些常式包括：  
  
-   純量值的使用者定義函數 (純量 UDF)  
  
-   資料表值使用者定義函數 (TVF)  
  
-   使用者定義程序 (UDP)  
  
-   使用者定義觸發程序  
  
 CLR 常式在 Managed 程式碼中包含三個相同的結構。 這三個結構會對應到類別的 public、static (在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET 中則為 shared) 方法。 除了常式之外，使用者定義型別 (UDT) 和使用者定義彙總函式也可以使用 .NET Framework 來定義。 UDT 和使用者定義彙總都會對應到整個 .NET Framework 類別。  
  
 .NET Framework 常式的每個類型都有一個 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 宣告，而且可以在能夠使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 對等項目之 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中的任何位置使用。 例如，純量 UDF 可以在任何純量運算式中使用。 TVF 可以在任何 FROM 子句中使用。 程序可以在 EXEC 陳述式中叫用，或從用戶端應用程式叫用。  
  
> [!NOTE]  
>  Common Language Runtime 上的 CLR 物件 (使用者定義函數、使用者定義類型或觸發程序) 可以在多個執行緒上執行 (平行計畫)，如果查詢最佳化工具判定這是有幫助的。 不過，如果使用者定義函數存取資料，則是以序列計畫執行。 在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 之前的伺服器版本上執行時，如果使用者定義函數包含 LOB 參數或傳回值，也必須以序列計畫執行。  
  
 下表列出此章節所涵蓋的主題。  
  
 [CLR 整合使用者入門](../../../relational-databases/clr-integration/database-objects/getting-started-with-clr-integration.md)  
 提供搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 CLR 整合編譯物件所需之程式庫與命名空間的簡短概觀。 包含範例 "Hello World" CLR 預存程序。  
  
 [支援的 .NET Framework 程式庫](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)  
 提供 CLR 整合支援之 .NET Framework 程式庫的相關資訊。  
  
 [CLR 整合程式設計模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
 提供 CLR 整合程式設計模型限制的相關資訊。  
  
 [.NET Framework 的 SQL Server 資料類型](../../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型及其 .NET Framework 對等項目的概觀。  
  
 [CLR 整合自訂屬性的概觀](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)  
 提供 CLR 整合自訂屬性的相關資訊。  
  
 [CLR 使用者定義函式](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 描述如何實作與使用各種類型的 CLR 函數：資料表值函式、純量函數，以及使用者定義彙總函式。  
  
 [CLR 使用者定義型別](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 描述如何實作及使用 CLR 使用者定義型別。  
  
 [CLR 預存程序](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)  
 描述如何實作及使用 CLR 預存程序。  
  
 [CLR 觸發程序](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
 描述如何實作及使用 CLR 觸發程序。  
  
## <a name="see-also"></a>另請參閱  
 [通用語言執行平台&#40;CLR&#41;整合概觀](../../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
  
  
