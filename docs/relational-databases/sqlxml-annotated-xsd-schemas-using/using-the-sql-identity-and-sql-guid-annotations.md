---
title: 使用 sql:identity 和 sql:guid 註解
description: 瞭解如何在 XSD 架構中使用 sql： identity 和 sql： guid 批註來定義 XML updategram 的行為。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:guid
- annotated XSD schemas, IDENTITY-type columns
- annotated XSD schemas, GUID values
- DiffGrams [SQLXML], annotations
- identity annotation
- XSD schemas [SQLXML], GUID values
- GUIDs [SQLXML]
- guid annotation
- sql:identity
- IDENTITY-type column
- XSD schemas [SQLXML], IDENTITY-type columns
- updategrams [SQLXML], GUID values
ms.assetid: 7661dfd0-6573-4692-a8f1-3597adcd33c4
author: MightyPen
ms.author: genemi
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7c66bac3f83aff00a458d3fed14296d2b03071f7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479319"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>使用 sql:identity 和 sql:guid 註解
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  您可以在對應至資料庫資料行的任何節點上，指定 XSD 架構中的 **sql： identity** 和 **sql： guid** 批註 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 Updategram 格式支援 **updg： identity** 和 **updg： guid** 屬性，而 DiffGram 格式則否。 **Updg： identity** 屬性會定義更新 identity 類型資料行的行為。 **Updg： guid** 屬性可讓您從取得 guid 值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並在 updategram 中使用它。 如需詳細資訊和工作範例，請參閱 [使用 XML Updategram 插入資料 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)。  
  
 **Sql： identity** 和 **sql： guid** 批註會將此功能延伸至 diffgram。  
  
 當您執行 DiffGram 時，會先將其轉換為 updategram，然後再執行 updategram。 藉由在 XSD 架構中指定 **sql： identity** 和 **sql： guid** 注釋，實際上會定義 updategram 的行為。 因此，所有註解的描述都在 updategram 的內容中。 註解可以同時用於 DiffGrams 和 updategrams，不過，updategrams 已經提供更強大的方式來處理識別與 GUID 值。  
  
 **Sql： identity** 和 **sql： guid** 批註可以定義在複雜內容元素上。  
  
## <a name="sqlidentity-annotation"></a>sql:identity 註解  
 您可以在對應到 IDENTITY 類型資料庫資料行的任何節點上，指定 XSD 架構中的 **sql： identity** 批註。 針對此批註指定的值會定義如何更新識別類型資料行 (使用 updategram 中提供的值來修改資料行，或略過值，在此情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在此資料行) 使用產生的值。  
  
 **Sql： identity** 批註可以指派兩個值：  
  
 ignore  
 導向 updategram 忽略 updategram 中針對該資料行提供的任何值，並依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生識別值。  
  
 useValue  
 導向 updategram 使用 updategram 中提供的值，來更新 IDENTITY 類型的資料行。 updategram 不會檢查資料行是否是識別值。  
  
 如果 updategram 為 IDENTITY 類型的資料行指定值，則必須在架構中指定 **sql： IDENTITY = "useValue"** 。  
  
## <a name="sqlguid-annotation"></a>sql:guid 註解  
 updategram 可以讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生 GUID 值，然後在 updategram 中使用此值。 在 Diffgram 的內容中，您可以使用 **sql： guid** 批註來指定是否要使用 SQL Server 所產生的 guid 值，或使用 updategram 中針對該資料行提供的值。  
  
 **Sql： guid** 批註可以指派兩個值：  
  
 generate  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所產生的 GUID 用於更新作業中的該資料行。  
  
 useValue  
 指定在 updategram 中指定的值用於該資料行。 這是預設值。  
  
  
