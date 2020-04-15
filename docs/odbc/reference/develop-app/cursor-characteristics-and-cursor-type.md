---
title: 游標特徵和游標類型 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301625"
---
# <a name="cursor-characteristics-and-cursor-type"></a>資料指標特性和資料指標類型
應用程式可以指定游標的特徵,而不是指定游標類型(僅轉發、靜態、鍵集驅動或動態)。 為此,應用程式在打開語句句柄上的游標之前選擇游標的可滾動性(通過設置SQL_ATTR_CURSOR_SCROLLABLE語句屬性)和靈敏度(通過設置SQL_ATTR_CURSOR_SENSITIVITY語句屬性)。 然後,驅動程式選擇最有效地提供應用程式請求的特徵的游標類型。  
  
 每當應用程式設置SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_SCROLLABLE、SQL_ATTR_CURSOR_SENSITIVITY 或SQL_ATTR_CURSOR_TYPE的任何語句屬性時,驅動程式都會對這組四個屬性中的其他語句屬性進行任何必需的更改,以便其值保持一致。 因此,當應用程式指定游標特徵時,驅動程式可以基於此隱式選擇更改指示游標類型的屬性;因此,驅動程式可以更改指示游標類型的屬性。當應用程式指定類型時,驅動程式可以更改任何其他屬性,以便與所選類型的特徵保持一致。 有關這些語句屬性的詳細資訊,請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函數說明。  
  
 設置語句屬性以指定游標類型和游標特徵的應用程式可能會獲取游標,而游標不是滿足應用程式要求的驅動程式上最有效的方法。  
  
 語句屬性的隱式設定是驅動程式定義的,只不過它必須遵循以下規則:  
  
-   僅轉發的遊標永遠不會滾動;請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)中SQL_ATTR_CURSOR_SCROLLABLE的定義。  
  
-   不敏感的遊標永遠不會被提升(因此它們併發是唯讀的);這是基於他們在 ISO SQL 標準中對不敏感游標的定義。  
  
 因此,語句屬性的隱式設置發生在下表中描述的情況下。  
  
|應用程式集屬性到|隱含設定的其他屬性|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY到SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITYSQL_INSENSITIVE。|  
|SQL_ATTR_CONCURRENCYSQL_CONCUR_LOCK、SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITYSQL_UNSPECIFIED或SQL_SENSITIVE,由驅動程式定義。 它永遠不會設置為SQL_INSENSITIVE,因為不敏感的游標始終是唯讀的。|  
|SQL_ATTR_CURSOR_SCROLLABLE到SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE到SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLESQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE到驅動程式指定的SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN 或SQL_CURSOR_DYNAMIC。 它永遠不會設置為SQL_CURSOR_FORWARD_ONLY。|  
|SQL_ATTR_CURSOR_SENSITIVITY到SQL_INSENSITIVE|SQL_ATTR_CONCURRENCYSQL_CONCUR_READ_ONLY。<br /><br /> SQL_ATTR_CURSOR_TYPESQL_CURSOR_STATIC。|  
|SQL_ATTR_CURSOR_SENSITIVITY到SQL_SENSITIVE|SQL_ATTR_CONCURRENCY驅動程式指定的SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES。 它永遠不會設置為SQL_CONCUR_READ_ONLY。<br /><br /> SQL_ATTR_CURSOR_TYPE驅動程式指定的SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN或SQL_CURSOR_DYNAMIC。|  
|SQL_ATTR_CURSOR_SENSITIVITY到SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY到驅動程式指定的SQL_CONCUR_READ_ONLY、SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES。<br /><br /> SQL_ATTR_CURSOR_TYPE驅動程式指定的SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN或SQL_CURSOR_DYNAMIC。|  
|SQL_ATTR_CURSOR_TYPE到SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLESQL_SCROLLABLE。<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY到SQL_SENSITIVE。 (但前提是SQL_ATTR_CONCURRENCY不等於SQL_CONCUR_READ_ONLY。 可向上的動態游標始終對在其自己的事務中所做的更改敏感。|  
|SQL_ATTR_CURSOR_TYPE到SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLESQL_NONSCROLLABLE。|  
|SQL_ATTR_CURSOR_TYPE到SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLESQL_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITYSQL_UNSPECIFIED或SQL_SENSITIVE(根據駕駛員定義的條件,如果SQL_ATTR_CONCURRENCY未SQL_CONCUR_READ_ONLY)。|  
|SQL_ATTR_CURSOR_TYPE到SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLESQL_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY到SQL_INSENSITIVE(如果SQL_ATTR_CONCURRENCYSQL_CONCUR_READ_ONLY)。<br /><br /> SQL_ATTR_SENSITIVITYSQL_UNSPECIFIED或SQL_SENSITIVE(如果SQL_ATTR_CONCURRENCY不SQL_CONCUR_READ_ONLY)。|
