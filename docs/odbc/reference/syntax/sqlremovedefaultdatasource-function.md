---
description: SQLRemoveDefaultDataSource 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0010e59cc4dfad2d54b8b1c4e59e83ea72fcd3ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487086"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函式
**一致性**  
 引進的版本： ODBC 1.0，已淘汰  
  
 **總結**  
 在 ODBC 3.0 中， **SQLRemoveDefaultDataSource**函數已由具有 ODBC_REMOVE_DEFAULT_DSN 之*fRequest*引數的[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)呼叫所取代。 如果 ODBC 2.x 安裝程式呼叫這個函式，*odbc 安裝程式* 會將它對應到下列 **SQLConfigDataSource** 呼叫：  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
