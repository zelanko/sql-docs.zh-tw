---
title: SQLRemoveDefaultDataSource 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDefaultDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDefaultDataSource
helpviewer_keywords:
- SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea540d2ef6747bbe3bfc9ac55f04afe1d63349f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537236"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函式
**合規性**  
 導入的版本：ODBC 1.0 時，已被取代  
  
 **摘要**  
 在 ODBC 3.0 **SQLRemoveDefaultDataSource**函式已取代呼叫[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)具有*常見*ODBC_REMOVE_DEFAULT_DSN 引數。 如果 ODBC 2 *.x*安裝程式會呼叫此函式，ODBC 安裝程式會將它對應至下列**SQLConfigDataSource**呼叫：  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
