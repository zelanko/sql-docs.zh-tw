---
title: 描述項控制代碼 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3aa085cc0a098f557ca7a8cbddcd787a178b79d0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711606"
---
# <a name="descriptor-handles"></a>描述項控制代碼
A*描述元*是描述 SQL 陳述式的參數或結果集的資料行的中繼資料的集合，所看到的應用程式或驅動程式 (也稱為*實作*)。 因此，可以填入任何四個角色描述元：  
  
-   **應用程式參數描述項 (APD)。** 包含應用程式緩衝區繫結到 SQL 陳述式中，例如其地址、 長度和 C 資料類型參數的相關資訊。  
  
-   **實作參數描述項 (IPD)。** 包含 SQL 陳述式，例如其 SQL 資料類型、 長度和 null 屬性中參數的相關資訊。  
  
-   **應用程式資料列描述項 (ARD)。** 包含應用程式緩衝區繫結至結果集，例如其地址、 長度和 C 資料類型中的資料行的相關資訊。  
  
-   **實作資料列描述項 (IRD)。** 包含在結果集中，例如其 SQL 資料類型、 長度和 null 屬性的資料行的相關資訊。  
  
 配置陳述式時，會自動配置 （一個填入每個角色） 的四個描述項。 這些值稱為*自動配置描述元*，而且永遠與該陳述式相關聯。 應用程式也可以將配置具有描述元**SQLAllocHandle**。 這些值稱為*明確配置描述元*。 它們配置在連線上，而且可以與該連線，以便滿足 APD 或 ARD 的角色，這些陳述式上的一或多個陳述式相關聯。  
  
 ODBC 中的大部分作業可以由應用程式執行而不需明確使用的描述元。 不過，描述項會提供方便的捷徑，針對某些作業。 例如，假設應用程式想要將資料從兩組不同的緩衝區。 若要使用第一個集合的緩衝區，它會重複呼叫**SQLBindParameter**若要將其繫結中的參數**插入**陳述式，然後執行陳述式。 若要使用第二組的緩衝區，它會重複此程序。 或者，它可以設定的繫結至第一個集合的緩衝區中有一個描述項和第二組中其他描述元的緩衝區。 若要繫結的資料集之間切換，應用程式只會呼叫**SQLSetStmtAttr**並正確描述元關聯為 APD 陳述式。  
  
 如需描述項的詳細資訊，請參閱[類型的描述元](../../../odbc/reference/develop-app/types-of-descriptors.md)。
