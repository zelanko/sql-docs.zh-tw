---
title: SQLRemoveDefaultDataSource 函式 |Microsoft 文件
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5b3a37cf0b0f42567d4a787b9c090f8298f74ca
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函式
**一致性**  
 版本引進了： ODBC 1.0，已被取代  
  
 **摘要**  
 在 ODBC 3.0 **SQLRemoveDefaultDataSource**函式已由呼叫取代[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)與*常見*ODBC_REMOVE_DEFAULT_DSN 引數。 如果 ODBC 2*.x*安裝程式會呼叫此函式，ODBC 安裝程式會將它對應至下列**SQLConfigDataSource**呼叫：  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
