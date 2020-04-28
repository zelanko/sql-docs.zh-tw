---
title: 描述項控制碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application parameter descriptor [ODBC]
- automatically allocated descriptors [ODBC]
- implementation row descriptor [ODBC]
- descriptor handles [ODBC]
- handles [ODBC], descriptor
- implementation parameter descriptor [ODBC]
- apd [ODBC]
- ard [ODBC]
- explicitly allocated descriptors [ODBC]
- ipd [ODBC]
- ird [ODBC]
- application row descriptor [ODBC]
ms.assetid: 7741035c-f3e7-4c89-901e-fe528392f67d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed0595c97f3f4ad92d976c89327a01e25cb5b753
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305909"
---
# <a name="descriptor-handles"></a>描述項控制代碼
描述*項是元*資料的集合，可描述 SQL 語句的參數或結果集的資料行，如同應用程式或驅動程式（也稱為「*執行*」）所見。 因此，描述元可以填入四個角色中的任何一個：  
  
-   **應用程式參數描述項（APD）。** 包含系結至 SQL 語句中的參數之應用程式緩衝區的相關資訊，例如其位址、長度和 C 資料類型。  
  
-   **實參數描述項（IPD）。** 包含 SQL 語句中參數的相關資訊，例如其 SQL 資料類型、長度和 null 屬性。  
  
-   **應用程式資料列描述項（ARD）。** 包含系結至結果集中資料行之應用程式緩衝區的相關資訊，例如其位址、長度和 C 資料類型。  
  
-   **執行資料列描述項（IRD）。** 包含結果集中資料行的相關資訊，例如其 SQL 資料類型、長度和 null 屬性。  
  
 配置語句時，會自動設定四個描述項（一個填滿每個角色）。 這些稱為自動設定的*描述*元，而且一律會與該語句相關聯。 應用程式也可以使用**SQLAllocHandle**來配置描述元。 這些稱為明確配置的*描述*元。 它們會在連接上配置，並可與該連接上的一或多個語句相關聯，以滿足 APD 或 ARD 在這些語句上的角色。  
  
 應用程式不需要明確使用描述元，即可執行 ODBC 中的大部分作業。 不過，描述項會針對某些作業提供方便的快捷方式。 例如，假設應用程式想要從兩組不同的緩衝區插入資料。 若要使用第一組緩衝區，它會重複呼叫**SQLBindParameter** ，以將它們系結至**INSERT**語句中的參數，然後執行語句。 若要使用第二組的緩衝區，它會重複此程式。 或者，它可以設定一個描述元中第一組緩衝區的系結，以及另一個描述元中第二組緩衝區的系結。 若要在系結集合之間切換，應用程式只需要呼叫**SQLSetStmtAttr** ，並將正確的描述項與語句建立關聯，做為 APD。  
  
 如需描述項的詳細資訊，請參閱[描述元的類型](../../../odbc/reference/develop-app/types-of-descriptors.md)。
