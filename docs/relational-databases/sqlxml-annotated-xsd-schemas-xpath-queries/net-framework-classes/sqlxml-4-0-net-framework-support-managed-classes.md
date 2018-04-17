---
title: SQLXML Managed 類別 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
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
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 98ce0bf10480b6920274b1ab8ace4c341330c3ae
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlxml-40-net-framework-support---managed-classes"></a>SQLXML 4.0.NET Framework 支援的 Managed 類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 支援的功能可讓您撰寫應用程式以便從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體存取 XML 資料、將資料置於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 環境、處理資料，以及將更新傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 
  
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML Managed 類別會在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 內部公開 SQLXML 4.0 的功能。 您可以利用 SQLXML Managed 類別撰寫 C# 應用程式來存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體中的 XML 資料、將資料帶到 .NET Framework 環境、處理資料，以及將更新傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 做為 DiffGram 來套用更新。 使用 SQLXML Managed 類別，將更新套用到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫時，您必須使用對應的結構描述。 如需實用範例，請參閱[存取.NET 環境中的 SQLXML 功能](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)。  
  
 若要搭配 SQLXML 4.0 使用 SQLXML Managed 類別，您必須安裝 Microsoft Visual Studio。  
  
> [!NOTE]  
>  .NET Framework 包含 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .NET 資料提供者。 此提供者可用於存取 .NET 環境中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，不過，它僅能處理傳統的 SQL 查詢 (也就是除了 FOR XML 查詢之外的關聯式資料庫查詢)。 您無法在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中執行 XML 範本或伺服器端的 XPath 查詢。  

 如需有關存取和修改資料中的資訊[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]內[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework，以及如何使用 DiffGrams 更新中的資料[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表，請參閱[.NET環境中存取SQLXML功能](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md).  
  
> [!NOTE]  
>  您也可以撰寫 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 應用程式，藉由使用 XML 大量載入來大量載入 XML 文件。 如需詳細資訊，請參閱[執行大量載入的 XML 資料&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)。 您必須在應用程式中加入 XML 大量載入 DLL (Xblkld4.dll) 的參考。 這是 COM DLL，Visual Studio .NET 會自動為其建立包裝函數程式庫。  
  
  本節提供範例應用程式，示範如何使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)]SQLXML Managed 類別：  
 [執行 SQL 查詢&#40;SQLXML Managed 類別&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)  
  [使用 ExecuteXMLReader 方法執行 SQL 查詢](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-by-using-the-executexmlreader-method.md)  
  [處理用戶端上的 XML &#40;SQLXML Managed 類別&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/processing-xml-on-the-client-side-sqlxml-managed-classes.md)  
  [執行 XPath 查詢&#40;SQLXML Managed 類別&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-sqlxml-managed-classes.md)  
  [執行含有命名空間的 XPath 查詢&#40;SQLXML Managed 類別&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md)  
  [使用 CommandText 屬性執行範本檔案](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandtext-property.md)  
  [利用 CommandStream 屬性執行範本檔案](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandstream-property.md)  
  [套用 XSL 轉換&#40;SQLXML Managed 類別&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)  
  

  
  
