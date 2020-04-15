---
title: SQL刪除預設資料來源函數 |微軟文件
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
ms.openlocfilehash: 952ace7d17e8bb5b4c824761b02e5c8a0895f519
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303939"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函式
**一致性**  
 版本介紹: ODBC 1.0, 已棄用  
  
 **摘要**  
 在 ODBC 3.0 中 **,SQLRemoveDefaultDataSource**函數已被對[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)的調用替換為 ODBC_REMOVE_DEFAULT_DSN的*fRequest*參數。 如果 ODBC 2 *.x*安裝程式呼叫此功能,ODBC 安裝程式將將其映射到以下**SQLConfigDataSource**呼叫:  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
