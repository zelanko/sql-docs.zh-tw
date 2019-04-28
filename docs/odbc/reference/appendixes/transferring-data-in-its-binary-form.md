---
title: 以二進位形式的資料傳輸 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 44bf8de8ea4c33a20a6159c5702db0b7eaee9eed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735044"
---
# <a name="transferring-data-in-its-binary-form"></a>以二進位形式傳輸資料
應用程式可以安全地在使用相同的 DBMS 和硬體平台的兩個資料來源之間傳輸資料 （在使用指定的 DBMS 內部形式）。 給定的資料片段，SQL 資料類型必須是相同的來源和目標資料來源。 SQL_C_BINARY C 資料類型。  
  
 當應用程式呼叫**SQLFetch**， **SQLFetchScroll**，或**SQLGetData**驅動程式來源的資料來源擷取資料，從資料擷取資料來源和傳輸，而無需轉換，類型 SQL_C_BINARY 的儲存體位置。 當應用程式呼叫**SQLBulkOperations**， **SQLExecute**， **SQLExecDirect**， **SQLPutData 或 SQLSetPos**將資料傳送至目標資料來源驅動程式會從儲存體位置擷取資料，並傳輸，而不需要轉換，到目標資料來源。  
  
> [!NOTE]  
>  以這種方式傳輸 （二進位資料除外） 的任何資料的應用程式不在 Dbms 之間的互通性。  
  
 **SQLCopyDesc**可用來複製來源 DBMS 中的資料列繫結，到目標 DBMS 中的參數繫結。
