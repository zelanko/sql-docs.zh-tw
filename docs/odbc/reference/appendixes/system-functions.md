---
description: 系統函式
title: 系統函數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- system functions [ODBC]
- functions [ODBC], system functions
ms.assetid: 36614b4c-e037-43ef-8692-67f4861b144d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1be058f5021c3f03242a09500150acd98cac8e70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386404"
---
# <a name="system-functions"></a>系統函式
下表列出 ODBC 純量函數集中包含的系統函數。 藉由使用 SQL_SYSTEM_FUNCTIONS 的*資訊類型*來呼叫**SQLGetInfo** ，應用程式可以決定驅動程式支援哪些系統函數。  
  
 表示為 *exp* 的引數可以是資料行的名稱、另一個純量函數的結果，或是常值，其中基礎資料類型可以表示為 SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL、SQL_DOUBLE、SQL_TYPE_DATE、SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 表示為值的引數可以是常 *值* 常數，其中基礎資料類型可以表示為 SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL、SQL_DOUBLE、SQL_TYPE_DATE、SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 傳回的值會以 ODBC 資料類型表示。  
  
|函式|描述|  
|--------------|-----------------|  
|**資料庫 ( ) **  (ODBC 1.0) |傳回對應于連接控制碼的資料庫名稱。 使用 SQL_CURRENT_QUALIFIER 連接選項呼叫 **SQLGetConnectOption** ，也可以使用 (資料庫的名稱。 ) |  
|**IFNull (** _exp_，_value_ **) ** (ODBC 1.0) |如果 *exp* 為 null，則會傳回 *值* 。 如果 *exp* 不是 null，則會傳回 *exp* 。 可能的資料類型或 *值* 類型必須與 *exp*的資料類型相容。|  
|**使用者 ( ) **  (ODBC 1.0) |傳回 DBMS 中的使用者名稱。  (使用者名稱也可以藉由指定資訊類型來 **SQLGetInfo** ： SQL_USER_NAME。 ) 這可能與登入名稱不同。|
