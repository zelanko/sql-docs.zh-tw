---
description: 以二進位形式傳輸資料
title: 以二進位格式傳送資料 |Microsoft Docs
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
ms.openlocfilehash: ec858729e76c1e360ec0933eca3a29ab17542f4f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386324"
---
# <a name="transferring-data-in-its-binary-form"></a>以二進位形式傳輸資料
應用程式可以安全地傳輸 (內部形式的資料，這些資料來源是由使用相同 DBMS 和硬體平臺的兩個數據源中指定的 DBMS) 。 針對指定的資料片段，SQL 資料類型在來源和目標資料來源中必須相同。 C 資料類型為 SQL_C_BINARY。  
  
 當應用程式呼叫 **SQLFetch**、 **SQLFetchScroll**或 **SQLGetData** 來從來源資料源中取出資料時，驅動程式會從資料來源中抓取資料，並將資料傳輸至類型 SQL_C_BINARY 的儲存位置，而不需要轉換。 當應用程式呼叫 **SQLBulkOperations**、 **SQLExecute**、 **SQLExecDirect**、 **SQLPutData 或 SQLSetPos** 來將資料傳送到目標資料來源時，驅動程式會從儲存位置抓取資料，並將它傳輸（不需要轉換）至目標資料來源。  
  
> [!NOTE]  
>  以這種方式傳送任何資料 (但不是二進位資料) 的應用程式，在 Dbms 之間無法互通。  
  
 **SQLCopyDesc** 可以用來將來源 dbms 的資料列系結複製到目標 dbms 中的參數系結。
