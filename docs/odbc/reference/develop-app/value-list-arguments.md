---
title: 值清單引數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 47ef5564ae56f04877aa33b4ffb0f1644aa4d605
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="value-list-arguments"></a>值清單引數
值清單引數包含要用來比對以逗號分隔值清單。 ODBC 目錄函數沒有引數-清單只有一個值： *TableType*引數中的**SQLTables**。 設定*TableType*至 null 指標會與相同設 SQL_ALL_TABLE_TYPES，列舉所有可能值清單的成員。 這個引數不會受到 SQL_ATTR_METADATA_ID 陳述式屬性。 如需詳細資訊，請參閱[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)函式描述。
