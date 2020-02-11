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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 646d2724489140080a673f31e22429cc7ca39d4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022110"
---
# <a name="value-list-arguments"></a>值清單引數
值清單引數是由用來比對的逗點分隔值清單所組成。 ODBC 目錄函數中只有一個值清單引數： **SQLTables**中的*TableType*引數。 將*TableType*設定為 null 指標就如同設定為 SQL_ALL_TABLE_TYPES，這會列舉值清單的所有可能成員。 這個引數不會受到 SQL_ATTR_METADATA_ID 語句屬性的影響。 如需詳細資訊，請參閱[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)函數描述。
