---
title: 描述符句柄 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305909"
---
# <a name="descriptor-handles"></a>描述項控制代碼
*描述符*是一組元數據,用於描述 SQL 語句的參數或結果集的列,如應用程式或驅動程式(也稱為*實現*)所示。 因此,描述符可以填充四個角色中的任何一個:  
  
-   **應用程式參數描述符 (APD)。** 包含有關綁定到 SQL 語句中參數的應用程式緩衝區的資訊,例如其位址、長度和 C 資料類型。  
  
-   **實現參數描述符 (IPD)。** 包含有關 SQL 語句中參數的資訊,例如其 SQL 資料類型、長度和空值。  
  
-   **應用程式行描述符 (ARD)。** 包含有關綁定到結果集中列的應用程式緩衝區的資訊,例如其位址、長度和 C 資料類型。  
  
-   **實現行描述符 (IRD)。** 包含有關結果集中列的資訊,例如其 SQL 數據類型、長度和空值。  
  
 分配語句時,將自動分配四個描述符(每個角色一個填充)。 這些稱為*自動分配的描述符*,並且始終與該語句相關聯。 應用程式還可以使用**SQLAllocHandle**分配描述符。 這些被稱為*顯示式配置的描述 。* 它們在連接上分配,並可以與該連接上的一個或多個語句相關聯,以履行 APD 或 ARD 在這些語句上的作用。  
  
 ODBC 中的大多數操作都可以執行,而無需應用程式顯示式使用描述符。 但是,描述符為某些操作提供了方便的快捷方式。 例如,假設應用程式希望插入來自兩組不同緩衝區的數據。 若要使用第一組緩衝區,它將重複調用**SQLBindparameter**將它們綁定到**INSERT**語句中的參數,然後執行該語句。 要使用第二組緩衝區,它將重複此過程。 或者,它可以在一個描述符中設置對第一組緩衝區的綁定,在另一個描述符中設置第二組緩衝區的綁定。 要在綁定集之間切換,應用程式只需調用**SQLSetStmtAttr**並將正確的描述符與語句關聯為 APD。  
  
 有關描述符的詳細資訊,請參考[描述符的類型](../../../odbc/reference/develop-app/types-of-descriptors.md)。
