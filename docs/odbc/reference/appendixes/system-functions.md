---
title: "系統函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- system functions [ODBC]
- functions [ODBC], system functions
ms.assetid: 36614b4c-e037-43ef-8692-67f4861b144d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1537c769de2c0f421ed533ea73d75a1578a10559
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="system-functions"></a>系統函數
下表列出 ODBC 純量函式集合中包含的系統函數。 藉由呼叫**SQLGetInfo**與*資訊類型*的 SQL_SYSTEM_FUNCTIONS，應用程式可以判斷驅動程式支援的系統函數。  
  
 引數表示為*exp*可以是名稱資料行、 將另一個純量函數或常值，其中基礎資料類型可能會表示為 SQL_NUMERIC SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL、 SQL_DOUBLE、 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 引數表示為*值*可以是常值常數，其中基礎資料類型可以表示為 SQL_NUMERIC SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL、 SQL_DOUBLE、 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 傳回的值會表示為 ODBC 資料類型。  
  
|函數|Description|  
|--------------|-----------------|  
|**資料庫 （)** (ODBC 1.0)|傳回對應至連接控制代碼的資料庫名稱。 (資料庫的名稱，也可以透過呼叫**SQLGetConnectOption**使用 SQL_CURRENT_QUALIFIER 連接選項。)|  
|**IFNULL (** *exp*，*值***)** (ODBC 1.0)|如果*exp*為 null，*值*傳回。 如果*exp*不是 null， *exp*傳回。 可能資料類型或類型*值*必須是相容的資料型別*exp*。|  
|**使用者 > （)** (ODBC 1.0)|DBMS 中傳回的使用者名稱。 (使用者名稱也會藉由提供**SQLGetInfo**藉由指定的資訊類型： SQL_USER_NAME。)這可以是不同的登入名稱。|

