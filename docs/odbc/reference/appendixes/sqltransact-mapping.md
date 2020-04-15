---
title: SQLTransact 對應 ( P)微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6aaa056fca860a70f81ad7c3a4cd8539512bc25d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304879"
---
# <a name="sqltransact-mapping"></a>SQLTransact 對應
**SQLTransact**現在被**SQLEndTran**替換。 這兩個函數之間的主要區別是**SQLEndTran**包含一個參數*HandleType,* 它指定要完成的工作範圍。 *HandleType*參數可以指定環境或連接句柄。 以下調**SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 對應  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 如果*連接句柄*不等於SQL_NULL_HDBC。 *ConnectHandle*參數設置為*hdbc*的值。  
  
 **SQL_Transact**映射到  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 如果*連接句柄*等於SQL_NULL_HDBC。 *環境句柄*參數設置為*henv*的值。  
  
 在前面的兩種情況下,*完成類型*參數設定為與*fType*相同的值。
