---
title: 使用 SQLXMLOLEDB 提供者 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sample applications [SQLXML]
- SQLXMLOLEDB Provider, samples
- ClientSideXML property
ms.assetid: fbcefac5-29c9-478b-b0e0-d510b593f446
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f71fffba9ccfff30188056d931fb08526ce43a75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895116"
---
# <a name="using-the-sqlxmloledb-provider-sqlxml-40"></a>使用 SQLXMLOLEDB 提供者 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本章節的主題提供了 ADO 範例應用程式來說明 SQLXMLOLEDB 提供者特定之屬性的使用。  
  
## <a name="application-requirements-for-sqlxmloledb-40-provider"></a>SQLXMLOLEDB 4.0 提供者的應用程式需求  
 若要建立可使用 SQLXMLOLEDB 4.0 的工作範例，您必須執行以下工作：  
  
1.  建立 Microsoft Visual Basic .exe 應用程式，並加入下列其中一個參考：  
  
    -   Microsoft ActiveX Data Objects 2.6 的程式庫  
  
    -   Microsoft ActiveX Data Objects 2.7 文件庫  
  
    -   Microsoft ActiveX Data Objects 2.8 程式庫  
  
2.  部署及安裝 SQLXML 4.0 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     For more information, see on [SQLXML 4.0 Programming Concepts](../../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md) and [Installing SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="in-this-section"></a>本節內容  
 [執行 SQL 查詢&#40;SQLXMLOLEDB 提供者&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md)  
 說明如何使用 ClientSideXML 和 xml 根屬性來執行 SQL 查詢。  
  
 [執行包含 SQL 查詢的範本&#40;SQLXMLOLEDB 提供者&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md)  
 說明如何使用 ClientSideXML 屬性。  
  
 [執行 XPath 查詢&#40;SQLXMLOLEDB 提供者&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md)  
 說明如何使用 ClientSideXML、 基底路徑，以及對應的結構描述屬性。  
  
 [執行含有命名空間的 XPath 查詢&#40;SQLXMLOLEDB 提供者&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md)  
 說明如何針對符合命名空間的結構描述執行查詢。  
  
 [執行包含 XPath 查詢的範本&#40;SQLXMLOLEDB 提供者&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-xpath-queries-sqlxmloledb-provider.md)  
 說明如何使用 SQL 查詢使用 ClientSideXML、 基底路徑，以及對應的結構描述屬性執行範本。  
  
 [套用 XSL 轉換&#40;SQLXMLOLEDB 提供者&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/applying-an-xsl-transformation-sqlxmloledb-provider.md)  
 說明如何使用中套用 XSL 轉換的 ClientSideXML 和 xsl 屬性。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 的系統需求](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)  
  
  
