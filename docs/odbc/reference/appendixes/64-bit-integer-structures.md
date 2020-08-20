---
description: 64 位元整數結構
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
ms.openlocfilehash: 13c57fc582b23c3ca10768c930d44ae758f1d3d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471241"
---
# <a name="64-bit-integer-structures"></a>64 位元整數結構
Microsoft C 編譯器上的 SQL_C_SBIGINT 和 SQL_C_UBIGINT 資料類型識別碼的 C 類型 _int64。 使用 Microsoft® C 編譯器以外的編譯器時，C 類型可能會不同。 如果編譯器以原生方式支援64位整數，則驅動程式或應用程式應該將 ODBCINT64 定義為原生64位整數類型。 如果編譯器原本不支援64位整數，應用程式或驅動程式可以定義下列結構，以確保它可以存取此資料：  
  
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
  
 這些結構應該對齊8位元組的界限，因為64位的整數會對齊8位元組的界限。
