---
title: "描述項控制代碼 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be9387fd0b34123e1a0b903795b1bf1e2106d725
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="descriptor-handles"></a>描述項控制代碼
A*描述元*偵測到的應用程式或驅動程式會描述 SQL 陳述式的參數或結果集的資料行的中繼資料集合 (也稱為*實作*)。 因此，描述元可以填滿任何四個角色：  
  
-   **應用程式參數描述項 (APD)。** 包含應用程式緩衝區繫結到 SQL 陳述式中，例如其地址、 長度和 C 資料類型參數的相關資訊。  
  
-   **實作參數描述項 (IPD)。** 包含 SQL 陳述式中，例如其 SQL 資料類型、 長度和 null 屬性參數的相關資訊。  
  
-   **應用程式資料列描述項 (ARD)。** 包含有關應用程式緩衝區繫結至結果集，例如其地址、 長度和 C 資料類型中的資料行資訊。  
  
-   **實作資料列描述項 (IRD)。** 包含在結果集中，例如其 SQL 資料類型、 長度和 null 屬性資料行的相關資訊。  
  
 配置陳述式時，會自動配置 （一個填入每個角色） 的四個描述項。 這些值稱為*自動配置描述元*而且一定是與該陳述式相關聯。 應用程式也可以將配置描述元與**SQLAllocHandle**。 這些值稱為*明確配置描述元*。 它們在連接上進行配置，而且可以在該連接來滿足這些陳述式的 APD 或 ARD 的角色上的一個或多個陳述式相關聯。  
  
 ODBC 中的大部分作業可以由應用程式執行而不需明確使用的描述項。 不過，描述會提供方便的捷徑執行某些作業。 例如，假設應用程式想要將資料從兩組不同的緩衝區。 若要使用第一個集合的緩衝區，它會重複呼叫**SQLBindParameter**中的參數繫結**插入**陳述式，然後執行陳述式。 若要使用第二個集合的緩衝區，它會重複此程序。 或者，它可以設定的繫結至第一個集合中一個描述元的緩衝區和緩衝區，另一個描述元中的第二個的集合。 若要切換的繫結的集合，應用程式只會呼叫**SQLSetStmtAttr**並正確描述元關聯 APD 陳述式。  
  
 如需描述元的詳細資訊，請參閱[類型的描述元](../../../odbc/reference/develop-app/types-of-descriptors.md)。
