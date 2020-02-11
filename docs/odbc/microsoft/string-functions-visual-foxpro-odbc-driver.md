---
title: 字串函式（Visual FoxPro ODBC Driver） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db1fbaffbee0f74625f4a11cad3b961f194e3829
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948770"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>字串函式 (Visual FoxPro ODBC Driver)
下表列出 Visual FoxPro ODBC 驅動程式支援的 ODBC 字串操作函式;當相同函式的 Visual FoxPro 文法與 ODBC 語法不同時，會列出對等的 Visual FoxPro。  
  
|ODBC 文法|Visual FoxPro 文法|  
|------------------|---------------------------|  
|ASCII *（string_exp）*|ASC *（string_exp）*|  
|CHAR *（code）*|CHR *（string_exp）*|  
|CONCAT *（string_exp1，string_exp2）*|*string_exp1 + string_exp2*|  
|差異 *（string_exp1、string_exp2）*||  
|INSERT *（string_exp1、start、length、string_exp2）*|內容 *（string_exp1、開始、長度、string_exp2）*|  
|LCASE *（string_exp）*|LOWER *（string_exp）*|  
|LEFT *（string_exp，count）*||  
|長度 *（string_exp）*|LEN *（string_exp）*|  
|LTRIM *（string_exp）*||  
|重複 *（string_exp、計數）*|複寫 *（string_exp、計數）*|  
|REPLACE *（string_exp1、string_exp2、string_exp3）*|STRTRAN *（string_exp1、string_exp2、string_exp3）*|  
|RIGHT *（string_exp，count）*||  
|RTRIM *（string_exp）*||  
|SOUNDEX *（string_exp）*||  
|空間 *（計數）*||  
|SUBSTRING *（string_exp、start、length）*|SUBSTR *（string_exp，開始，長度）*|  
|UCASE *（string_exp）*|上限 *（string_exp）*|
