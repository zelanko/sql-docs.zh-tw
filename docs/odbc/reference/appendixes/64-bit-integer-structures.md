---
title: 64 位整數結構 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1ecbe4dae4c1bd21ac3d542ee0d9b18169df0116
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307509"
---
# <a name="64-bit-integer-structures"></a>64 位元整數結構
_int64,_int64 microsoft C 編譯器上SQL_C_SBIGINT和SQL_C_UBIGINT數據類型標識符的 C 類型。 當使用 Microsoft 以外的編譯器® C 編譯器時,C 類型可能不同。 如果編譯器本機支援 64 位元整數,則驅動程式或應用程式應將 ODBCINT64 定義為本機 64 位元整數類型。 如果編譯器本機不支援 64 位元整數,則應用程式或驅動程式可以定義以下結構,以確保它有權存取此資料:  
  
```  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLUINTEGER dwHighWord;  
} SQLUBIGINT  
  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLINTEGER sdwHighWord;  
} SQLBIGINT  
```  
  
 這些結構應與 8 位元組邊界對齊,因為 64 位整數與 8 位元組邊界對齊。
