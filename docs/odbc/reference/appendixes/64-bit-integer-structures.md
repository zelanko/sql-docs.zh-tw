---
title: 64位整數結構 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307509"
---
# <a name="64-bit-integer-structures"></a>64 位元整數結構
Microsoft C 編譯器上的 SQL_C_SBIGINT 和 SQL_C_UBIGINT 資料類型識別碼的 C 類型是 _int64。 當使用 Microsoft® C 編譯器以外的編譯器時，C 類型可能會不同。 如果編譯器原本就支援64位整數，則驅動程式或應用程式應該將 ODBCINT64 定義為原生64位整數類型。 如果編譯器原本就不支援64位整數，應用程式或驅動程式可以定義下列結構，以確保它具有此資料的存取權：  
  
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
  
 這些結構應該對齊8個位元組的界限，因為64位整數對齊8個位元組的界限。
