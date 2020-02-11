---
title: 使用 sql:identity 和 sql:guid 註解
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 50483d7f6f84371b42bf0c79fbc74a1f85a65eab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75246824"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>使用 sql:identity 和 sql:guid 註解
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您可以在對應至中資料庫資料行的任何節點上，于 XSD 架構中指定**sql： identity**和**sql： guid**批註。 Updategram 格式支援**updg： identity**和**updg： guid**屬性，而 DiffGram 格式則否。 **Updg： at identity**屬性會定義更新 identity 類型資料行時的行為。 **Updg： guid**屬性可讓您從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]取得 guid 值，並在 updategram 中使用它。 如需詳細資訊和工作範例，請參閱[使用 XML Updategram 插入資料 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)。  
  
 **Sql： identity**和**sql： guid**批註會將此功能延伸至 diffgram。  
  
 當您執行 DiffGram 時，會先將其轉換為 updategram，然後再執行 updategram。 藉由在 XSD 架構中指定**sql： identity**和**sql： guid**批註，您實際上是定義 updategram 的行為。 因此，所有註解的描述都在 updategram 的內容中。 註解可以同時用於 DiffGrams 和 updategrams，不過，updategrams 已經提供更強大的方式來處理識別與 GUID 值。  
  
 **Sql： identity**和**sql： guid**批註可以在複雜的 content 元素上定義。  
  
## <a name="sqlidentity-annotation"></a>sql:identity 註解  
 您可以在對應到 IDENTITY 類型之資料庫資料行的任何節點上，于 XSD 架構中指定**sql： identity**注釋。 針對此批註指定的值會定義如何更新 IDENTITY 類型的資料行（藉由使用 updategram 中提供的值來修改資料行，或忽略值，在此情況下[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，會針對此資料行使用產生的值）。  
  
 **Sql： identity**注釋可以被指派兩個值：  
  
 ignore  
 導向 updategram 忽略 updategram 中針對該資料行提供的任何值，並依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生識別值。  
  
 useValue  
 導向 updategram 使用 updategram 中提供的值，來更新 IDENTITY 類型的資料行。 updategram 不會檢查資料行是否是識別值。  
  
 如果 updategram 指定 IDENTITY 類型資料行的值，則必須在架構中指定**sql： IDENTITY = "useValue"** 。  
  
## <a name="sqlguid-annotation"></a>sql:guid 註解  
 updategram 可以讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生 GUID 值，然後在 updategram 中使用此值。 在 Diffgram 的內容中，您可以使用**sql： guid**注釋，指定是否要使用 SQL Server 所產生的 guid 值，或使用該資料行的 updategram 中所提供的值。  
  
 **Sql： guid**注釋可以被指派兩個值：  
  
 generate  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所產生的 GUID 用於更新作業中的該資料行。  
  
 useValue  
 指定在 updategram 中指定的值用於該資料行。 這是預設值。  
  
  
