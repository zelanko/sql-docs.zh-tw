---
title: 值清單引數 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306739"
---
# <a name="value-list-arguments"></a>值清單引數
值清單引數是由用來比對的逗點分隔值清單所組成。 ODBC 目錄函數中只有一個值清單引數： **SQLTables**中的*TableType*引數。 將*TableType*設定為 null 指標就如同設定為 SQL_ALL_TABLE_TYPES，這會列舉值清單的所有可能成員。 這個引數不會受到 SQL_ATTR_METADATA_ID 語句屬性的影響。 如需詳細資訊，請參閱[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)函數描述。
