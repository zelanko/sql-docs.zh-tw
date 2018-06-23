---
title: SQLXML Managed 類別 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- .NET Framework [SQLXML], Managed Classes
- SQL Server .NET Data Provider
- Managed Classes [SQLXML], about managed classes
- providers [SQLXML], SQL Server .NET Data Provider
- data providers [SQLXML], SQL Server .NET Data Provider
- Managed Classes [SQLXML]
- XML [SQLXML]
- SQLXML Managed Classes
- providers [SQLXML], SQLXML Managed Classes
- data providers [SQLXML], SQLXML Managed Classes
- SQLXML, Managed Classes
ms.assetid: 73a5faeb-dabf-4895-acb5-a9651b646065
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b43ad8fb5fa88eb18fb0b5d5e41caecc04f99928
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034101"
---
# <a name="sqlxml-managed-classes"></a>SQLXML Managed 類別
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML Managed 類別會在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 內部公開 SQLXML 4.0 的功能。 您可以利用 SQLXML Managed 類別撰寫 C# 應用程式來存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體中的 XML 資料、將資料帶到 .NET Framework 環境、處理資料，以及將更新傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 做為 DiffGram 來套用更新。 使用 SQLXML Managed 類別，將更新套用到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫時，您必須使用對應的結構描述。 如需實用範例，請參閱[存取.NET 環境中的 SQLXML 功能](accessing-sqlxml-functionality-in-the-net-environment.md)。  
  
 若要搭配 SQLXML 4.0 使用 SQLXML Managed 類別，您必須安裝 Microsoft Visual Studio。  
  
> [!NOTE]  
>  .NET Framework 包含 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .NET 資料提供者。 此提供者可用於存取 .NET 環境中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，不過，它僅能處理傳統的 SQL 查詢 (也就是除了 FOR XML 查詢之外的關聯式資料庫查詢)。 您無法在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中執行 XML 範本或伺服器端的 XPath 查詢。  
  
## <a name="in-this-section"></a>本節內容  
 [SQLXML Managed 類別物件模型](../../../database-engine/dev-guide/sqlxml-managed-classes-object-model.md)  
 記載 SQLXML Managed 類別及其屬性和方法。  
  
 [使用 SQLXML Managed 類別](sqlxml-4-0-net-framework-support-managed-classes.md)  
 提供使用 SQLXML Managed 類別的範例。  
  
  