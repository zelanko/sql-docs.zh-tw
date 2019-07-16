---
title: '使用 sql: identity 和 sql: guid 註解 |Microsoft Docs'
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
ms.openlocfilehash: 1a6c19e23fc886e15b8e116ca293c4560fded74e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066877"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>使用 sql:identity 和 sql:guid 註解
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以指定**sql: identity**並**sql: guid**對應至資料庫資料行中的任何節點上的 XSD 結構描述中的註解[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 而 updategram 格式支援**updg： 在身分識別**並**updg: guid**屬性，DiffGram 格式則否。 **Updg： 在身分識別**屬性更新 IDENTITY 類型資料行定義的行為。 **Updg: guid**屬性可讓您取得的 GUID 值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和在 updategram 中使用它。 如需詳細資訊和實用範例，請參閱 <<c0> [ 插入的資料使用 XML Updategram &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)。</c0>  
  
 **Sql: identity**並**sql: guid**註解會將此功能擴充到 DiffGrams。  
  
 當您執行 DiffGram 時，會先將其轉換為 updategram，然後再執行 updategram。 藉由指定**sql: identity**並**sql: guid** XSD 結構描述中的註解，您是在實際上就在定義 updategram 的行為。 因此，所有註解的描述都在 updategram 的內容中。 註解可以同時用於 DiffGrams 和 updategrams，不過，updategrams 已經提供更強大的方式來處理識別與 GUID 值。  
  
 **Sql: identity**並**sql: guid**註解可以在複雜內容元素上定義。  
  
## <a name="sqlidentity-annotation"></a>sql:identity 註解  
 您可以指定**sql: identity**對應到 IDENTITY 類型的資料庫資料行的任何節點上的 XSD 結構描述中的註釋。 針對此註解指定的值可讓您定義如何更新 IDENTITY 類型資料行 (使用 updategram 中提供的值來修改資料行，或忽略值，在此情況下[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-產生的值用於此資料行)。  
  
 **Sql: identity**註解可以指派兩個值：  
  
 ignore  
 導向 updategram 忽略 updategram 中針對該資料行提供的任何值，並依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生識別值。  
  
 useValue  
 導向 updategram 使用 updategram 中提供的值，來更新 IDENTITY 類型的資料行。 updategram 不會檢查資料行是否是識別值。  
  
 如果 updategram 指定 IDENTITY 類型資料行的值**sql: identity ="useValue"** 必須指定結構描述中。  
  
## <a name="sqlguid-annotation"></a>sql:guid 註解  
 updategram 可以讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生 GUID 值，然後在 updategram 中使用此值。 在 DiffGrams 的內容，您可以使用**sql: guid**註解來指定是否要使用 SQL Server 所產生的 GUID 值，或使用 updategram 中針對該資料行提供的值。  
  
 **Sql: guid**註解可以指派兩個值：  
  
 generate  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所產生的 GUID 用於更新作業中的該資料行。  
  
 useValue  
 指定在 updategram 中指定的值用於該資料行。 這是預設值。  
  
  
