---
title: 資料指標的特性和資料指標類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbef278f3f25b572ddc44e87d60b5cdcd33058c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043823"
---
# <a name="cursor-characteristics-and-cursor-type"></a>資料指標特性和資料指標類型
應用程式可以指定資料指標，而不是指定資料指標類型 （順向、 靜態、 索引鍵集驅動或動態） 的特性。 若要這樣做，應用程式當時的 （藉由設定 SQL_ATTR_CURSOR_SCROLLABLE 陳述式屬性） 的資料指標的可捲動性和敏感度 （藉由設定 SQL_ATTR_CURSOR_SENSITIVITY 陳述式屬性） 開啟的陳述式上的資料指標控制代碼。 驅動程式選擇最有效率的方式，提供特性的資料指標類型要求的應用程式。  
  
 每當應用程式設定的任何陳述式屬性 sql_attr_concurrency 設定、 SQL_ATTR_CURSOR_SCROLLABLE、 SQL_ATTR_CURSOR_SENSITIVITY，還是 SQL_ATTR_CURSOR_TYPE，驅動程式對任何必要的變更在這組的其他陳述式屬性四個屬性，讓它們的值都保持一致。 如此一來，當應用程式指定的資料指標特性時，驅動程式可以變更屬性，指出這個隱含的選取範圍; 為基礎的資料指標類型當應用程式指定的類型，驅動程式可以變更任何其他屬性，以便符合所選類型的特性。 如需有關這些陳述式屬性的詳細資訊，請參閱 < [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函式描述。  
  
 應用程式設定來指定資料指標類型和資料指標的特性的陳述式屬性執行取得不是最有效率的方法提供該驅動程式符合應用程式的需求的資料指標的風險。  
  
 陳述式屬性的隱含設定驅動程式-定義不同之處在於它必須遵守下列規則：  
  
-   順向資料指標絕對是可捲動;請參閱 SQL_ATTR_CURSOR_SCROLLABLE 中定義[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
-   非感應式資料指標絕對是不可更新 （和其並行因此處於唯讀狀態）;這根據其定義的非感應式資料指標中的 ISO SQL 標準。  
  
 因此，陳述式屬性的隱含設定就會發生在下表中所述的案例。  
  
|應用程式設定屬性|隱含地設定其他屬性|  
|-----------------------------------|-------------------------------------|  
|SQL_CONCUR_READ_ONLY 的 SQL_ATTR_CONCURRENCY|為 SQL_INSENSITIVE SQL_ATTR_CURSOR_SENSITIVITY。|  
|若要 SQL_CONCUR_LOCK、 SQL_CONCUR_ROWVER、 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED 或 SQL_SENSITIVE，驅動程式所定義。 它可以永遠不會設定為 SQL_INSENSITIVE，因為非感應式資料指標永遠是唯讀。|  
|為 SQL_NONSCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE|SQL_CURSOR_FORWARD_ONLY 的 SQL_ATTR_CURSOR_TYPE|  
|為 SQL_SCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC、 SQL_CURSOR_KEYSET_DRIVEN，或 SQL_CURSOR_DYNAMIC，所指定的驅動程式。 它永遠不會設定為 SQL_CURSOR_FORWARD_ONLY。|  
|SQL_ATTR_CURSOR_SENSITIVITY 為 SQL_INSENSITIVE|若要 SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY。<br /><br /> 若要 SQL_CURSOR_STATIC SQL_ATTR_CURSOR_TYPE。|  
|SQL_ATTR_CURSOR_SENSITIVITY 至 SQL_SENSITIVE|Sql_attr_concurrency SQL_CONCUR_LOCK、 SQL_CONCUR_ROWVER、 或 SQL_CONCUR_VALUES，驅動程式所指定的設定。 它永遠不會設定為 SQL_CONCUR_READ_ONLY。<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY、 SQL_CURSOR_STATIC、 SQL_CURSOR_KEYSET_DRIVEN，或 SQL_CURSOR_DYNAMIC，所指定的驅動程式。|  
|SQL_ATTR_CURSOR_SENSITIVITY 至 SQL_UNSPECIFIED|Sql_attr_concurrency SQL_CONCUR_READ_ONLY、 SQL_CONCUR_LOCK、 SQL_CONCUR_ROWVER、 或 SQL_CONCUR_VALUES，驅動程式所指定的設定。<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY、 SQL_CURSOR_STATIC、 SQL_CURSOR_KEYSET_DRIVEN，或 SQL_CURSOR_DYNAMIC，所指定的驅動程式。|  
|SQL_CURSOR_DYNAMIC 的 SQL_ATTR_CURSOR_TYPE|為 SQL_SCROLLABLE SQL_ATTR_SCROLLABLE。<br /><br /> 若要 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY。 （但是只有 SQL_ATTR_CONCURRENCY 不等於 SQL_CONCUR_READ_ONLY。 可更新動態資料指標永遠是他們自己的交易中所做的變更影響。）|  
|SQL_CURSOR_FORWARD_ONLY 的 SQL_ATTR_CURSOR_TYPE|為 SQL_NONSCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE。|  
|SQL_CURSOR_KEYSET_DRIVEN 的 SQL_ATTR_CURSOR_TYPE|為 SQL_SCROLLABLE SQL_ATTR_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 或 SQL_SENSITIVE （根據驅動程式所定義的條件，如果 SQL_ATTR_CONCURRENCY 不 SQL_CONCUR_READ_ONLY）。|  
|SQL_CURSOR_STATIC 的 SQL_ATTR_CURSOR_TYPE|為 SQL_SCROLLABLE SQL_ATTR_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY 為 SQL_INSENSITIVE （如果 sql_attr_concurrency 設定為 SQL_CONCUR_READ_ONLY）。<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 或 SQL_SENSITIVE （如果 SQL_ATTR_CONCURRENCY 不 SQL_CONCUR_READ_ONLY）。|
