---
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
ms.openlocfilehash: ca71687887444cafc502c15683f3972cf6308e6b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302829"
---
# <a name="system-functions"></a>系統函數
下表列出 ODBC 純量函數集所包含的系統函數。 藉由使用 SQL_SYSTEM_FUNCTIONS 的*資訊類型*呼叫**SQLGetInfo** ，應用程式可以判斷驅動程式支援哪些系統函數。  
  
 表示為*exp*的引數可以是資料行的名稱、另一個純量函數的結果，或常值，其中基礎資料類型可能會表示為 SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL、SQL_DOUBLE、SQL_TYPE_DATE、SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 表示為 value 的引數可以是常*值*常數，其中基礎資料類型可以表示為 SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL、SQL_DOUBLE、SQL_TYPE_DATE、SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 傳回的值會以 ODBC 資料類型表示。  
  
|函式|描述|  
|--------------|-----------------|  
|**DATABASE （）** （ODBC 1.0）|傳回對應至連接控制碼的資料庫名稱。 （您也可以使用 SQL_CURRENT_QUALIFIER 連接選項呼叫**SQLGetConnectOption**來取得資料庫的名稱。）|  
|**IFNull （** _exp_，_value_**）** （ODBC 1.0）|如果*exp*是 null，則會傳回*值*。 如果*exp*不是 null，則會傳回*exp* 。 可能的資料類型或*值*類型必須與*exp*的資料類型相容。|  
|**USER （）** （ODBC 1.0）|傳回 DBMS 中的使用者名稱。 （藉由指定資訊類型，也可以透過**SQLGetInfo**來取得使用者名稱： SQL_USER_NAME）。這可能與登入名稱不同。|
