---
title: "64 位元整數結構 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b267e536535d0df75e1f7c048baa31099c97a704
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="64-bit-integer-structures"></a>64 位元整數的結構
SQL_C_SBIGINT 和 SQL_C_UBIGINT 資料類型識別項在 Microsoft C 編譯器的 C 類型是 _int64。 使用其他比 Microsoft （) C 編譯器的編譯器時，C 類型可能會不同。 如果編譯器原生支援 64 位元整數，驅動程式或應用程式應該定義 ODBCINT64 原生 64 位元整數型別。 編譯器不原生支援 64 位元整數，如果應用程式或驅動程式可以定義下列的結構，以確定它擁有這項資料的存取：  
  
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
