---
title: 64 位元整數結構 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac1a80e94d225b26cf879b27bdb0e138e0b0d1d9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306327"
---
# <a name="64-bit-integer-structures"></a>64 位元整數結構
SQL_C_SBIGINT 和 SQL_C_UBIGINT 資料型別識別項在 Microsoft C 編譯器的 C 類型是 _int64。 使用其他比 Microsoft （) C 編譯器的編譯器時，C 類型可能會不同。 如果編譯器以原生方式支援 64 位元整數，驅動程式或應用程式應該定義 ODBCINT64 原生的 64 位元整數型別。 編譯器不以原生方式支援 64 位元整數，如果應用程式或驅動程式就可以定義下列的結構，以確定它有存取此資料：  
  
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
  
 這些結構應該對齊 8 位元組界限，因為 64 位元整數被對齊 8 位元組界限。
