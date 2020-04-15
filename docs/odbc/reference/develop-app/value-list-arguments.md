---
title: 值清單參數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd655bd745c3bb06923e047d4134b286cf64703e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306739"
---
# <a name="value-list-arguments"></a>值清單引數
值清單參數由用於匹配的逗號分隔值列表組成。 ODBC 目錄函數中只有一個值清單參數 **:SQLTables**中的*表類型*參數。 將*表類型*設置為空指標與將其設置為SQL_ALL_TABLE_TYPES相同,後者枚舉值清單的所有可能成員。 此參數不受SQL_ATTR_METADATA_ID語句屬性的影響。 有關詳細資訊,請參閱[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)函數說明。
