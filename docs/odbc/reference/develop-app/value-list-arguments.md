---
title: "值清單引數 |Microsoft 文件"
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
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 15604e317105982c5011b31096934e32bea98e11
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="value-list-arguments"></a>值清單引數
值清單引數包含要用來比對以逗號分隔值清單。 ODBC 目錄函數沒有引數-清單只有一個值： *TableType*引數中的**SQLTables**。 設定*TableType*至 null 指標會與相同設 SQL_ALL_TABLE_TYPES，列舉所有可能值清單的成員。 這個引數不會受到 SQL_ATTR_METADATA_ID 陳述式屬性。 如需詳細資訊，請參閱[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)函式描述。
