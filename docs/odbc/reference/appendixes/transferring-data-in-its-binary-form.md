---
title: 以二進位形式傳輸資料 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2897f882dc9dcd78ee8b919de01126d6be510c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070019"
---
# <a name="transferring-data-in-its-binary-form"></a>以二進位形式傳輸資料
應用程式可以安全地在使用相同 DBMS 和硬體平臺的兩個數據源之間傳輸資料（在指定 DBMS 所使用的內部表單中）。 對於指定的資料片段而言，來源和目標資料來源中的 SQL 資料類型必須相同。 C 資料類型為 SQL_C_BINARY。  
  
 當應用程式呼叫**SQLFetch**、 **SQLFetchScroll**或**SQLGetData**來抓取來源資料源中的資料時，驅動程式會從資料來源抓取資料，並將它傳送至 SQL_C_BINARY 類型的儲存位置，而不會進行轉換。 當應用程式呼叫**SQLBulkOperations**、 **SQLExecute**、 **SQLExecDirect**、 **SQLPutData 或 SQLSetPos**將資料傳送至目標資料來源時，驅動程式會從儲存位置抓取資料，並將它傳輸至目標資料來源，而不需要轉換。  
  
> [!NOTE]  
>  以這種方式傳送任何資料（二進位資料除外）的應用程式無法在 Dbms 間互通。  
  
 **SQLCopyDesc**可以用來將來源 dbms 的資料列系結複製到目標 dbms 中的參數系結。
