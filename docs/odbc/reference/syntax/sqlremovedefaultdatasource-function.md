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
ms.openlocfilehash: cfefcd9f2f55e2d78c5c6e5b1bac7ce52e9033e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68024602"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函式
**標準**  
 引進的版本： ODBC 1.0，已被取代  
  
 **摘要**  
 在 ODBC 3.0 中，已使用 ODBC_REMOVE_DEFAULT_DSN 的*fRequest*引數呼叫[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)來取代**SQLRemoveDefaultDataSource**函數。 如果 ODBC 2.x 安裝程式呼叫此函式，*odbc 安裝程式*會將它對應至下列**SQLConfigDataSource**呼叫：  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
