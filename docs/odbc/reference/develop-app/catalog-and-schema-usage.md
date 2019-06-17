---
title: 目錄和結構描述使用方式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9476f4f928890514354f97ce604f871bd8a06d11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63007886"
---
# <a name="catalog-and-schema-usage"></a>目錄和結構描述的使用方式
資料來源不一定支援目錄與結構描述名稱做為所有的 SQL 陳述式中的物件名稱識別項。 資料來源可能支援類別目錄和結構描述名稱，在一或多個 SQL 陳述式的下列類別：資料操作語言 (DML) 陳述式、 程序呼叫中，資料表定義陳述式、 索引定義陳述式和權限定義陳述式。 若要判斷哪一個類別目錄和結構描述中可以使用名稱的 SQL 陳述式的類別，應用程式會呼叫**SQLGetInfo**使用 SQL_CATALOG_USAGE 和 SQL_SCHEMA_USAGE 選項。
