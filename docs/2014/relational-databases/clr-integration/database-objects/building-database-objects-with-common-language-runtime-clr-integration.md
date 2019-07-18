---
title: 建立使用 Common Language Runtime (CLR) 整合的資料庫物件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8dc507d455636bf6256fd7ba4649dba53d32884e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919248"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>利用 Common Language Runtime (CLR) 整合建置資料庫物件
  您可以建置使用的資料庫物件[!INCLUDE[ssNoVersion](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]稱為 「 CLR 常式 」。 這些常式包括：  
  
-   純量值的使用者定義函數 (純量 UDF)  
  
-   資料表值使用者定義函數 (TVF)  
  
-   使用者定義程序 (UDP)  
  
-   使用者定義觸發程序  
  
 CLR 常式在 Managed 程式碼中包含三個相同的結構。 這三個結構會對應到類別的 public、static (在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET 中則為 shared) 方法。 除了常式之外，使用者定義型別 (UDT) 和使用者定義彙總函式也可以使用 .NET Framework 來定義。 UDT 和使用者定義彙總都會對應到整個 .NET Framework 類別。  
  
 每種類型的.NET Framework 常式都[!INCLUDE[tsql](../../../includes/ssnoversion-md.md)]，[!INCLUDE[tsql](../../../includes/tsql-md.md)]可以使用對等項目。 例如，純量 UDF 可以在任何純量運算式中使用。 TVF 可以在任何 FROM 子句中使用。 程序可以在 EXEC 陳述式中叫用，或從用戶端應用程式叫用。  
  
> [!NOTE]  
>  Common Language Runtime 上的 CLR 物件 (使用者定義函數、使用者定義類型或觸發程序) 可以在多個執行緒上執行 (平行計畫)，如果查詢最佳化工具判定這是有幫助的。 不過，如果使用者定義函數存取資料，則是以序列計畫執行。 在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 之前的伺服器版本上執行時，如果使用者定義函數包含 LOB 參數或傳回值，也必須以序列計畫執行。  
  
 下表列出此章節所涵蓋的主題。  
  
 [CLR 整合使用者入門](getting-started-with-clr-integration.md)  
 提供搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 CLR 整合編譯物件所需之程式庫與命名空間的簡短概觀。 包含範例 "Hello World" CLR 預存程序。  
  
 [支援的 .NET Framework 程式庫](supported-net-framework-libraries.md)  
 提供 CLR 整合支援之 .NET Framework 程式庫的相關資訊。  
  
 [CLR 整合程式設計模型限制](clr-integration-programming-model-restrictions.md)  
 提供 CLR 整合程式設計模型限制的相關資訊。  
  
 [.NET Framework 的 SQL Server 資料類型](../../clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型及其 .NET Framework 對等項目的概觀。  
  
 [CLR 整合自訂屬性的概觀](../../../database-engine/dev-guide/overview-of-clr-integration-custom-attributes.md)  
 提供 CLR 整合自訂屬性的相關資訊。  
  
 [CLR 使用者定義函式](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 描述如何實作與使用各種類型的 CLR 函數：資料表值函式、純量函數，以及使用者定義彙總函式。  
  
 [CLR 使用者定義型別](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 描述如何實作及使用 CLR 使用者定義型別。  
  
 [CLR 預存程序](../../../database-engine/dev-guide/clr-stored-procedures.md)  
 描述如何實作及使用 CLR 預存程序。  
  
 [CLR 觸發程序](../../../database-engine/dev-guide/clr-triggers.md)  
 描述如何實作及使用 CLR 觸發程序。  
  
## <a name="see-also"></a>另請參閱  
 [通用語言執行平台&#40;CLR&#41;整合概觀](../common-language-runtime-integration-overview.md)  
  
  
