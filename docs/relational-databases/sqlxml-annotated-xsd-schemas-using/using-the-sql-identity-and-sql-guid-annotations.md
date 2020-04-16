---
title: 使用 sql:identity 和 sql:guid 註解
description: 瞭解如何在 XSD 架構中使用 sql:標識和 sql:guid 註釋來定義 XML 更新圖的行為。
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
ms.openlocfilehash: f581c1a5c0d925d48df5a16d95cdb141e2d48f83
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388100"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>使用 sql:identity 和 sql:guid 註解
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以在映射到[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的資料庫列的任何節點上的 XSD 架構中指定**sql:標識**和**sql:guid**註解。 更新格格式支援**updg:在識別**和**updg:guid**屬性,而 DiffGram 格式不支援。 **updg:在標識**屬性定義更新 IDENTITY 類型列時的行為。 **updg:guid**屬性允許您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從 獲取 GUID 值並在更新圖中使用。 有關詳細資訊和工作範例,請參閱使用[XML 更新圖插入資料&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)。  
  
 **sql:標識**和**sql:guid**註解將此功能擴展到 DiffGram。  
  
 當您執行 DiffGram 時，會先將其轉換為 updategram，然後再執行 updategram。 通過在 XSD 架構中指定**sql:標識**和**sql:guid**註釋,實際上是在定義更新語法的行為。 因此，所有註解的描述都在 updategram 的內容中。 註解可以同時用於 DiffGrams 和 updategrams，不過，updategrams 已經提供更強大的方式來處理識別與 GUID 值。  
  
 **sql:標識**和**sql:guid**註釋可以在複雜的內容元素上定義。  
  
## <a name="sqlidentity-annotation"></a>sql:identity 註解  
 您可以在映射到 IDENTITY 類型資料庫列的任何節點上的 XSD 架構中指定**sql:標識**註釋。 為此註釋指定的值定義如何更新 IDENTITY 類型列(通過使用更新圖中提供的值來修改列,或者忽略該值,在這種情況下,此列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將使用 生成的值)。  
  
 可以配置**sql:識別**註釋兩個值:  
  
 ignore  
 導向 updategram 忽略 updategram 中針對該資料行提供的任何值，並依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生識別值。  
  
 useValue  
 導向 updategram 使用 updategram 中提供的值，來更新 IDENTITY 類型的資料行。 updategram 不會檢查資料行是否是識別值。  
  
 如果更新圖指定了 IDENTITY 類型列的值,則必須在架構中指定**sql:identity_"使用值"。**  
  
## <a name="sqlguid-annotation"></a>sql:guid 註解  
 updategram 可以讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生 GUID 值，然後在 updategram 中使用此值。 在 DiffGram 的上下文中,可以使用**sql:guid**註釋指定是使用 SQL Server 生成的 GUID 值,還是使用該列的更新語法中提供的值。  
  
 可以配置**sql:guid**註解兩個值:  
  
 generate  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所產生的 GUID 用於更新作業中的該資料行。  
  
 useValue  
 指定在 updategram 中指定的值用於該資料行。 這是預設值。  
  
  
