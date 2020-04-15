---
title: 以二進位形式傳輸數據 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], transferring in binary form
- transferring data in binary form [ODBC]
- binary data transfers [ODBC]
ms.assetid: 4b12a9de-51d0-416a-87f4-9bf84959cad9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53531ff4a3b2e1441fabf22ec7a3ce12b15540eb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301410"
---
# <a name="transferring-data-in-its-binary-form"></a>以二進位形式傳輸資料
應用程式可以在使用同一 DBMS 和硬體平臺的兩個數據源之間安全地傳輸數據(以指定的 DBMS 使用的內部形式)。 對於給定的數據段,SQL 數據類型在源和目標數據源中必須相同。 C 數據類型SQL_C_BINARY。  
  
 當應用程式呼叫**SQLFetch、SQLFetchScroll**或**SQLGetData**從來源資料來源檢索資料時,驅動程式會從資料源檢索資料,並將其傳輸到SQL_C_BINARY類型的儲存位置,**SQLFetchScroll**而無需轉換。 當應用程式呼叫**SQLBulk 操作**、SQLExecute、SQLExecDirect、SQLPutData**或 SQLSetPos**將資料發送到目標資料來源時,驅動程式將從儲存位置檢索資料,並將其傳輸到目標資料**SQLExecute****SQLExecDirect**來源,而無需轉換。  
  
> [!NOTE]  
>  以這種方式傳輸任何資料(二進位數據除外)的應用程式在 DBMS 之間不可互通。  
  
 **SQLCopyDesc**可用於將行綁定從源 DBMS 複製到目標 DBMS 中的參數綁定。
