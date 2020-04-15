---
title: 系統功能 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302829"
---
# <a name="system-functions"></a>系統函數
下表列出了 ODBC 標量函數集中中包含的系統函數。 通過使用*SQL_SYSTEM_FUNCTIONS的資訊類型*呼叫**SQLGetInfo,** 應用程式可以確定驅動程式支援哪些系統功能。  
  
 表示為*exp*的參數可以是列的名稱、另一個標量函數的結果或文本,其中基礎數據類型可以表示為SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL、SQL_DOUBLE、SQL_TYPE_DATE、SQL_TYPE_TIME或SQL_TYPE_TIMESTAMP。  
  
 表示為*值*的參數可以是文本常量,其中基礎數據類型可以表示為SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL、SQL_DOUBLE、SQL_TYPE_DATE、SQL_TYPE_TIME或SQL_TYPE_TIMESTAMP。  
  
 返回的值表示為 ODBC 數據類型。  
  
|函式|描述|  
|--------------|-----------------|  
|**資料庫(** ODBC 1.0)|返回與連接句柄對應的資料庫的名稱。 (資料庫的名稱也可通過使用SQL_CURRENT_QUALIFIER連接選項調用**SQLGetConnectOption**獲得。|  
|**IFNULL(**_爆炸_,_數值_**) (ODBC** 1.0)|如果*exp*為 null,則傳回*值*。 如果*exp*不是 null,則傳回*exp。* 可能的資料類型或*值*類型必須與*exp*的資料類型相容。|  
|**使用者(** ODBC 1.0)|返回 DBMS 中的使用者名稱。 (通過指定資訊類型:SQL_USER_NAME,SQLGetInfo 也可通過**使用者名**獲得使用者名。這可能與登錄名不同。|
