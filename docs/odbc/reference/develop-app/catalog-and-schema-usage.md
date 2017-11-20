---
title: "類別目錄和結構描述 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 217f68d674dc7099b741e77d287ca81fcc2688e5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="catalog-and-schema-usage"></a>類別目錄和結構描述的使用方式
資料來源不一定支援類別目錄和結構描述名稱做為所有的 SQL 陳述式中的物件名稱識別碼。 資料來源可能支援類別目錄和結構描述名稱中一或多個 SQL 陳述式的下列類別： 資料操作語言 (DML) 陳述式、 程序呼叫中，資料表定義陳述式、 索引定義陳述式和權限定義陳述式。 若要判斷哪一個類別目錄和結構描述中可以使用名稱的 SQL 陳述式的類別，應用程式呼叫**SQLGetInfo**與 SQL_CATALOG_USAGE 和 SQL_SCHEMA_USAGE 選項。

