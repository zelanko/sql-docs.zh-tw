---
title: 資料指標特性和資料指標類型 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8354fdabf6830780ec2d128492c86cc1edd582ac
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301625"
---
# <a name="cursor-characteristics-and-cursor-type"></a>資料指標特性和資料指標類型
應用程式可以指定資料指標的特性，而不是指定資料指標類型（順向、靜態、索引鍵集驅動或動態）。 若要這樣做，應用程式會選取資料指標的捲動（藉由設定 SQL_ATTR_CURSOR_SCROLLABLE 語句屬性）和敏感度（藉由設定 SQL_ATTR_CURSOR_SENSITIVITY 語句屬性），然後才在語句控制碼上開啟資料指標。 然後，驅動程式會選擇最有效率地提供應用程式所要求之特性的游標類型。  
  
 每當應用程式設定任何語句屬性 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_SCROLLABLE、SQL_ATTR_CURSOR_SENSITIVITY 或 SQL_ATTR_CURSOR_TYPE 時，驅動程式會對這四個屬性集中的其他語句屬性進行任何必要的變更，讓它們的值保持一致。 如此一來，當應用程式指定資料指標特性時，驅動程式就可以根據這個隱含的選取範圍，變更表示資料指標類型的屬性。當應用程式指定類型時，驅動程式可以變更任何其他屬性，以與所選類型的特性一致。 如需這些語句屬性的詳細資訊，請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函數描述。  
  
 設定語句屬性來指定資料指標類型和資料指標特性的應用程式，會執行取得資料指標的風險，而該驅動程式並不是符合應用程式需求的最有效率方法。  
  
 語句屬性的隱含設定是驅動程式定義的，不同之處在于它必須遵循下列規則：  
  
-   順向資料指標永遠不會滾動;請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)中的 SQL_ATTR_CURSOR_SCROLLABLE 定義。  
  
-   不區分資料指標永遠不會更新（因此它們的並行處理是唯讀的）;這是以 ISO SQL 標準中不區分資料指標的定義為基礎。  
  
 因此，語句屬性的隱含設定會出現在下表所述的案例中。  
  
|應用程式集合屬性為|隱含設定的其他屬性|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY 至 SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE。|  
|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES|如驅動程式所定義，SQL_UNSPECIFIED 或 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY。 它永遠不能設定為 SQL_INSENSITIVE，因為不區分的資料指標永遠是唯讀的。|  
|SQL_ATTR_CURSOR_SCROLLABLE 至 SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE 至 SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE 至 SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC，如同驅動程式所指定。 它永遠不會設定為 SQL_CURSOR_FORWARD_ONLY。|  
|SQL_ATTR_CURSOR_SENSITIVITY 至 SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY。<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC。|  
|SQL_ATTR_CURSOR_SENSITIVITY 至 SQL_SENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，如同驅動程式所指定。 它永遠不會設定為 SQL_CONCUR_READ_ONLY。<br /><br /> 如驅動程式所指定，SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE。|  
|SQL_ATTR_CURSOR_SENSITIVITY 至 SQL_UNSPECIFIED|如驅動程式所指定，SQL_CONCUR_READ_ONLY、SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY。<br /><br /> 如驅動程式所指定，SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE。|  
|SQL_ATTR_CURSOR_TYPE 至 SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE。<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY SQL_SENSITIVE。 （但僅限 SQL_ATTR_CONCURRENCY 不等於 SQL_CONCUR_READ_ONLY。 可更新的動態資料指標對自己的交易中所做的變更一律是敏感的。）|  
|SQL_ATTR_CURSOR_TYPE 至 SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE SQL_NONSCROLLABLE。|  
|SQL_ATTR_CURSOR_TYPE 至 SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY，SQL_UNSPECIFIED 或 SQL_SENSITIVE （根據驅動程式定義的準則，如果 SQL_ATTR_CONCURRENCY 不是 SQL_CONCUR_READ_ONLY）。|  
|SQL_ATTR_CURSOR_TYPE 至 SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY SQL_INSENSITIVE （如果 SQL_ATTR_CONCURRENCY 是 SQL_CONCUR_READ_ONLY）。<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 或 SQL_SENSITIVE （如果 SQL_ATTR_CONCURRENCY 不是 SQL_CONCUR_READ_ONLY）。|
