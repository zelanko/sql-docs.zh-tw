---
title: "書籤 C 資料類型 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1013d3307b1fea0d5460c2dce1caf10556804233
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="bookmark-c-data-type"></a>書籤 C 資料類型
書籤 C 資料類型可讓應用程式擷取書籤。 書籤 C 類型只能用於擷取書籤的值可以是可變長度。它們不應該轉換成其他資料型別。 應用程式擷取從資料行 0 的結果集的書籤**SQLBulkOperations** （與 SQL_ADD 的作業）， **SQLFetch**， **SQLFetchScroll**，或**SQLGetData**。 如需詳細資訊，請參閱[書籤](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
 下表列出的值*CType*書籤 C 資料類型，可實作書籤 C 資料類型，與這項資料的定義的 ODBC C 資料類型則是從 SQL 類型。H.  
  
> [!NOTE]  
>  SQL_C_BOOKMARK 資料型別已被取代。 ODBC 3*.x*應用程式不應該使用 SQL_C_BOOKMARK。 ODBC 3*.x*驅動程式需要他們想要使用的 ODBC 2 時，才支援 SQL_C_BOOKMARK。*x*使用它的應用程式。 驅動程式管理員會將 SQL_C_VARBOOKMARK 對應至 SQL_C_BOOKMARK 中，當應用程式搭配 ODBC 2。*x*驅動程式。  
  
|C 類型識別碼|ODBC C typedef|C 類型|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(已被取代)|書籤|不帶正負號的 long int|  
|SQL_C_VARBOOKMARK|SQLCHAR *|不帶正負號 char *|

