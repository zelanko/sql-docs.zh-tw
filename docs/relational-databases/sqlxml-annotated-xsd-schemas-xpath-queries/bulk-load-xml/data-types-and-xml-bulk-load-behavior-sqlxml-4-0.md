---
title: 資料類型與 XML 大量載入行為（SQLXML）
description: 瞭解 SQLXML 4.0 中的資料類型和 XML 大量載入行為。
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4e247ae58867054a1051f58f8a17d0d1ef701b2e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790666"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>資料類型與 XML 大量載入行為 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  通常會忽略對應架構（XSD 或 XDR 類型和**sql： datatype**）中指定的資料類型，但下列情況除外：  
  
 在 XSD 中：  
  
-   如果類型是**dateTime**或**time**，您必須指定**SQL： Datatype** ，因為 XML 大量載入會先執行資料轉換，然後再將資料傳送給 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
-   當您在中將大量載入到**uniqueidentifier**類型的資料行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，而且 XSD 值是包含大括弧（{和}）的 GUID 時，您必須指定**sql： datatype = "uniqueidentifier"** ，以在將值插入資料行之前移除大括弧。 如果未指定**sql： datatype** ，則會以大括弧傳送值，而插入作業會失敗。  
  
 如需**sql： datatype**的詳細資訊，請參閱[資料類型強制型轉和 Sql： DATATYPE 注釋 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 在 XDR 中：  
  
-   如果**dt： type**是**datetime**、 **time**、 **dateTime.tz**或**time.tz**，您必須同時指定**DT： Type**和**sql： datatype**資料類型，因為 XML 大量載入會先執行資料轉換，然後再將資料傳送至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
-   如果您的 XML 資料類型為**uuid**，則必須指定**sql： datatype** ;**dt： type = "uuid"** 也是必要的，除非資料是字串資料。 如果您未指定**dt： uuid**，XML 大量載入會接受具有大括弧的字串（並在必要時移除它們）。  
  
-   如果 XML 資料為**bin**或 **. hex**，則您必須指定具有**dt： type**的 xml 資料類型。 接著，XML 大量載入會將資料載入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，做為資料的十六進位表示法。  
  
  
