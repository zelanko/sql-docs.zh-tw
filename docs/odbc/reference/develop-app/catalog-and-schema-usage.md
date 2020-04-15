---
title: 目錄和架構使用方式 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 245bd007f070a94689283830ba7a1362e31353e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306249"
---
# <a name="catalog-and-schema-usage"></a>目錄和結構描述的使用方式
數據源不一定支援目錄和架構名稱作為所有 SQL 語句中的物件名稱識別符。 數據源可能支援以下一類或多個 SQL 語句中的目錄和架構名稱:資料操作語言 (DML) 語句、過程呼叫、表定義語句、索引定義語句和特權定義語句。 要確定可以使用目錄和架構名稱的 SQL 語句的類,應用程式使用 SQL_CATALOG_USAGE 和SQL_SCHEMA_USAGE選項調用**SQLGetInfo。**
