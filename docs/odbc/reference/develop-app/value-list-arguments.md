---
description: 值清單引數
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
ms.openlocfilehash: fd2f2e970ea94635cda0b43b741abfda1130645b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421412"
---
# <a name="value-list-arguments"></a>值清單引數
值清單引數包含要用於比對的逗點分隔值清單。 ODBC 目錄函數中只有一個值清單引數： **SQLTables**中的*TableType*引數。 如果將 *TableType* 設定為 null 指標，則會將它設定為 SQL_ALL_TABLE_TYPES，以列舉值清單的所有可能成員。 SQL_ATTR_METADATA_ID 語句屬性不會影響這個引數。 如需詳細資訊，請參閱 [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) 函數描述。
