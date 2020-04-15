---
title: SQLBindParam 對應 ( P)微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1df595722297c91dc75398470912188e109e278
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305438"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 對應
**SQLBindParam**不能真正稱為棄用,因為它在 ODBC 中從未存在過;但是,它仍然表示重複的功能 - 驅動程式管理員需要匯出它,因為 ISO 和符合開放組的應用程式將使用它。 由於**SQLBind 參數**包含**SQLBindParam**的所有功能,因此**SQLBindParam**將映射到**SQLBind 參數**之上(當基礎驅動程式是 ODBC *3.x*驅動程式時)。 ODBC *3.x*驅動程式不需要實現**SQLBindParam**。  
  
## <a name="remarks"></a>備註  
 當對**SQLBindParam**進行以下調用時:  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 驅動程式管理員在驅動程式中呼叫**SQLBind 參數**,如下所示:  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 如果應用程式將在 64 位元作業系統上執行,請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另請參閱  
 [對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
