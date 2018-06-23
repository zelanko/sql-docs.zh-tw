---
title: 使用 SQLXMLOLEDB 提供者 (SQLXML 4.0) |Microsoft 文件
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
- sample applications [SQLXML]
- SQLXMLOLEDB Provider, samples
- ClientSideXML property
ms.assetid: fbcefac5-29c9-478b-b0e0-d510b593f446
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 37cfc512f02bef664756bf6d46574479112b7efa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146259"
---
# <a name="using-the-sqlxmloledb-provider-sqlxml-40"></a>使用 SQLXMLOLEDB 提供者 (SQLXML 4.0)
  本章節的主題提供了 ADO 範例應用程式來說明 SQLXMLOLEDB 提供者特定之屬性的使用。  
  
## <a name="application-requirements-for-sqlxmloledb-40-provider"></a>SQLXMLOLEDB 4.0 提供者的應用程式需求  
 若要建立可使用 SQLXMLOLEDB 4.0 的工作範例，您必須執行以下工作：  
  
1.  建立 Microsoft Visual Basic .exe 應用程式，並加入下列其中一個參考：  
  
    -   Microsoft ActiveX Data Objects 2.6 程式庫  
  
    -   Microsoft ActiveX Data Objects 2.7 程式庫  
  
    -   Microsoft ActiveX Data Objects 2.8 程式庫  
  
2.  部署及安裝 SQLXML 4.0 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。  
  
     如需詳細資訊，請參閱上[SQLXML 4.0 程式設計概念](../../sqlxml/sqlxml-4-0-programming-concepts.md)和[安裝 SQL Server Native Client](../../native-client/applications/installing-sql-server-native-client.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [執行 SQL 查詢&#40;SQLXMLOLEDB 提供者&#41;](executing-sql-queries-sqlxmloledb-provider.md)  
 說明如何 ClientSideXML 和 xml 根屬性來執行 SQL 查詢使用。  
  
 [執行包含 SQL 查詢的範本&#40;SQLXMLOLEDB 提供者&#41;](executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md)  
 說明如何 ClientSideXML 屬性使用。  
  
 [執行 XPath 查詢&#40;SQLXMLOLEDB 提供者&#41;](executing-xpath-queries-sqlxmloledb-provider.md)  
 說明如何使用 ClientSideXML、 基底路徑和對應的結構描述屬性。  
  
 [執行含有命名空間的 XPath 查詢&#40;SQLXMLOLEDB 提供者&#41;](executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md)  
 說明如何針對符合命名空間的結構描述執行查詢。  
  
 [執行包含 XPath 查詢的範本&#40;SQLXMLOLEDB 提供者&#41;](executing-templates-that-contain-xpath-queries-sqlxmloledb-provider.md)  
 說明如何使用 SQL 查詢使用 ClientSideXML、 基底路徑和對應的結構描述屬性執行範本。  
  
 [套用 XSL 轉換&#40;SQLXMLOLEDB 提供者&#41;](applying-an-xsl-transformation-sqlxmloledb-provider.md)  
 說明如何使用 ClientSideXML 和 xsl 屬性在套用 XSL 轉換。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 的系統需求](../../native-client/system-requirements-for-sql-server-native-client.md)  
  
  