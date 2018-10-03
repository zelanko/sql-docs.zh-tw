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
ms.openlocfilehash: 048db455419d2b74658b758f3a3c525b02bf37f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811406"
---
# <a name="system-functions"></a>系統函數
下表列出 ODBC 純量函式集合中包含的系統函數。 藉由呼叫**SQLGetInfo**具有*資訊類型*的 SQL_SYSTEM_FUNCTIONS，應用程式可以判斷驅動程式支援哪些系統函式。  
  
 引數可以分成*exp*可以是資料行名稱的另一個純量函式或常值，結果其中可能表示基礎資料類型為 SQL_NUMERIC SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL、 SQL_DOUBLE、 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 引數可以分成*值*可以是常值的常數，其中表示基礎資料類型，為 SQL_NUMERIC SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL、 SQL_DOUBLE、 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 傳回值會表示為 ODBC 資料類型。  
  
|函數|描述|  
|--------------|-----------------|  
|**資料庫 （)** (ODBC 1.0)|傳回對應至連接控制代碼的資料庫名稱。 (資料庫的名稱，也可以透過呼叫**SQLGetConnectOption** SQL_CURRENT_QUALIFIER 連接選項。)|  
|**IFNULL (** *exp*，*值 * * *)** (ODBC 1.0)|如果*exp*為 null，然後*值*會傳回。 如果*exp*不是 null， *exp*會傳回。 可能資料類型或類型*值*必須是相容的資料型別*exp*。|  
|**使用者 > （)** (ODBC 1.0)|DBMS 中傳回的使用者名稱。 (使用者名稱也是可透過**SQLGetInfo**藉由指定的資訊類型： SQL_USER_NAME。)這可以是不同的登入名稱。|
