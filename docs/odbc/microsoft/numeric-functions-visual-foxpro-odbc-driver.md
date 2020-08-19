---
description: 數值函式 (Visual FoxPro ODBC Driver)
title: 數值函式 (Visual FoxPro ODBC 驅動程式) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c8728446decd8a0ad04f08d88475ae08a7c69c5f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449370"
---
# <a name="numeric-functions-visual-foxpro-odbc-driver"></a>數值函式 (Visual FoxPro ODBC Driver)
下表說明 Visual FoxPro ODBC 驅動程式所支援的 ODBC 數值函式;當相同函式的 Visual FoxPro 文法與 ODBC 語法不同時，會列出 Visual FoxPro 對等專案。  
  
|ODBC 文法|Visual FoxPro 文法|  
|------------------|---------------------------|  
|ABS * (numeric_exp) *||  
|ACOS * (float_exp) *||  
|ASIN * (float_exp) *||  
|ATAN * (float_exp) *||  
|ATAN2 * (float_exp1 float_exp2) *|ATN2 (*float_exp1 float_exp2*) |  
|* (numeric_exp) *上限||  
|COS * (float_exp) *||  
|COT * (float_exp) *||  
|度數 * (numeric_exp) *|RTOD * (numeric_exp) *|  
|EXP * (float_exp) *||  
|樓層 * (numeric_exp) *||  
|記錄 * (float_exp) *||  
|LOG10 * (float_exp) *||  
|MOD * (integer_exp1 integer_exp2) *||  
|PI * ( ) *||  
|弧度 * (numeric_exp) *|DTOR * (numeric_exp) *|  
|RAND * ( [integer_exp] ) *||  
|四捨五入 * (numeric_exp，integer_exp) *||  
|簽署 * (numeric_exp) *||  
|SIN * (float_exp) *||  
|SQRT * (float_exp) *||  
|TAN * (float_exp) *||  
  
 不支援下列數值函數：  
  
 POWER * (numeric_exp integer_exp) *  
  
 截斷 * (numeric_exp，integer_exp) *
