---
description: SQLTransact 對應
title: SQLTransact 對應 |Microsoft Docs
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
ms.openlocfilehash: cf1298c9881a207c21074e03e8b0597ab8f11448
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429499"
---
# <a name="sqltransact-mapping"></a>SQLTransact 對應
**SQLTransact** 現在已由 **SQLEndTran**取代。 這兩個函式之間的主要差異在於， **SQLEndTran** 包含引數 *HandleType*，可指定要完成之工作的範圍。 *HandleType*引數可以指定環境或連接控制碼。 下列 **SQLTransact**呼叫：  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 對應至  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 如果 *ConnectionHandle* 不等於 SQL_Null_HDBC。 *ConnectionHandle*引數設定為*hdbc*的值。  
  
 **SQL_Transact** 對應至  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 如果 *ConnectionHandle* 等於 SQL_Null_HDBC。 *EnvironmentHandle*引數設定為*henv*的值。  
  
 在上述兩個案例中， *CompletionType* 引數都會設定為與 *fType*相同的值。
