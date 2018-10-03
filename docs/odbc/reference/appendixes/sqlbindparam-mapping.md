---
title: SQLBindParam 對應 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26f9bdc0564b98132bb5ec413c99917e78e4d62e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855176"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 對應
**SQLBindParam**無法真正呼叫已被取代因為它永遠不會有在 ODBC 中; 不過，它仍代表重複的功能 — 驅動程式管理員必須將它匯出，因為 ISO 和相容開啟群組的應用程式將會使用它。 因為**SQLBindParameter**包含的所有功能**SQLBindParam**， **SQLBindParam**將對應的**SQLBindParameter**(基礎驅動程式時 ODBC 3 *.x*驅動程式)。 ODBC 3 *.x*驅動程式不需要實作**SQLBindParam**。  
  
## <a name="remarks"></a>備註  
 當下列呼叫來**SQLBindParam**進行：  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 此驅動程式管理員會呼叫**SQLBindParameter**在驅動程式中，如下所示：  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)，如果您的應用程式會在 64 位元作業系統上執行。  
  
## <a name="see-also"></a>另請參閱  
 [對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
