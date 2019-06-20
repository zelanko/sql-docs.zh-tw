---
title: 系統函式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5870cb445d7afd098aba32ffd9be7a88c048bae5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735054"
---
# <a name="system-functions"></a>系統函數
下表列出 ODBC 純量函式集合中包含的系統函數。 藉由呼叫**SQLGetInfo**具有*資訊類型*的 SQL_SYSTEM_FUNCTIONS，應用程式可以判斷驅動程式支援哪些系統函式。  
  
 引數可以分成*exp*可以是資料行名稱的另一個純量函式或常值，結果其中可能表示基礎資料類型為 SQL_NUMERIC SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL、 SQL_DOUBLE、 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 引數可以分成*值*可以是常值的常數，其中表示基礎資料類型，為 SQL_NUMERIC SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL、 SQL_DOUBLE、 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 傳回值會表示為 ODBC 資料類型。  
  
|函數|描述|  
|--------------|-----------------|  
|**DATABASE( )**  (ODBC 1.0)|傳回對應至連接控制代碼的資料庫名稱。 (資料庫的名稱，也可以透過呼叫**SQLGetConnectOption** SQL_CURRENT_QUALIFIER 連接選項。)|  
|**IFNULL(** _exp_,_value_ **)**  (ODBC 1.0)|如果*exp*為 null，然後*值*會傳回。 如果*exp*不是 null， *exp*會傳回。 可能資料類型或類型*值*必須是相容的資料型別*exp*。|  
|**USER( )**  (ODBC 1.0)|DBMS 中傳回的使用者名稱。 (使用者名稱也是可透過**SQLGetInfo**藉由指定的資訊類型：SQL_USER_NAME。)這可以是不同的登入名稱。|
