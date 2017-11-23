---
title: "SQLBindParam 對應 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 14af02864d6e0810ffa6ffa49a35bf676c000aea
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 對應
**SQLBindParam**無法真正呼叫已被取代因為它永遠不會有在 ODBC 中; 不過，它仍代表重複的功能 — 驅動程式管理員必須將它匯出，因為 ISO 和相容開啟群組的應用程式將會使用它。 因為**SQLBindParameter**包含的所有功能**SQLBindParam**， **SQLBindParam**將最上層的對應**SQLBindParameter**(基礎驅動程式時 ODBC 3*.x*驅動程式)。 ODBC 3*.x*驅動程式不需要實作**SQLBindParam**。  
  
## <a name="remarks"></a>備註  
 下列呼叫來**SQLBindParam**進行：  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 驅動程式管理員呼叫**SQLBindParameter**驅動程式，如下所示：  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)，如果您的應用程式將在 64 位元作業系統上執行。  
  
## <a name="see-also"></a>請參閱＜  
 [對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
