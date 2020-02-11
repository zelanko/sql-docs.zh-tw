---
title: 數值函數（Visual FoxPro ODBC Driver） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC numeric functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], numeric functions
- numeric functions [ODBC]
- FoxPro ODBC driver [ODBC], numeric functions
ms.assetid: 7caab48e-cbb5-4bbc-a09b-5cf902e5bc45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 34d2ceb19bce2e466ff5cae7647125e94fdb7c03
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68044992"
---
# <a name="numeric-functions-visual-foxpro-odbc-driver"></a>數值函式 (Visual FoxPro ODBC Driver)
下表描述的是 Visual FoxPro ODBC 驅動程式所支援的 ODBC 數值函數;當相同函式的 Visual FoxPro 文法與 ODBC 語法不同時，會列出對等的 Visual FoxPro。  
  
|ODBC 文法|Visual FoxPro 文法|  
|------------------|---------------------------|  
|ABS *（numeric_exp）*||  
|ACOS *（float_exp）*||  
|ASIN *（float_exp）*||  
|ATAN *（float_exp）*||  
|ATAN2 *（float_exp1，float_exp2）*|ATN2 （*float_exp1，float_exp2*）|  
|上限 *（numeric_exp）*||  
|COS *（float_exp）*||  
|COT *（float_exp）*||  
|度數 *（numeric_exp）*|RTOD *（numeric_exp）*|  
|EXP *（float_exp）*||  
|樓層 *（numeric_exp）*||  
|記錄 *（float_exp）*||  
|LOG10 *（float_exp）*||  
|MOD *（integer_exp1，integer_exp2）*||  
|PI *（）*||  
|弧度 *（numeric_exp）*|DTOR *（numeric_exp）*|  
|RAND *（[integer_exp]）*||  
|ROUND *（numeric_exp，integer_exp）*||  
|SIGN *（numeric_exp）*||  
|SIN *（float_exp）*||  
|SQRT *（float_exp）*||  
|TAN *（float_exp）*||  
  
 不支援下列數值函數：  
  
 電源 *（numeric_exp、integer_exp）*  
  
 截斷 *（numeric_exp、integer_exp）*
