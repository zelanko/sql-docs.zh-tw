---
description: 字串函式 (Visual FoxPro ODBC Driver)
title: 字串函式 (Visual FoxPro ODBC 驅動程式) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ab2ecefb604183b0387a561f72494028c62d15f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471540"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>字串函式 (Visual FoxPro ODBC Driver)
下表列出 Visual FoxPro ODBC 驅動程式所支援的 ODBC 字串操作函數;當相同函式的 Visual FoxPro 文法與 ODBC 語法不同時，會列出 Visual FoxPro 對等專案。  
  
|ODBC 文法|Visual FoxPro 文法|  
|------------------|---------------------------|  
|ASCII * (string_exp) *|ASC * (string_exp) *|  
|CHAR * (程式碼) *|CHR * (string_exp) *|  
|CONCAT * (string_exp1，string_exp2) *|*string_exp1 + string_exp2*|  
|差異 * (string_exp1、string_exp2) *||  
|INSERT * (string_exp1、start、length、string_exp2) *|* (string_exp1、開始、長度 string_exp2*的內容) |  
|LCASE * (string_exp) *|較低的 * (string_exp) *|  
|左方 * (string_exp，count) *||  
|長度 * (string_exp) *|LEN * (string_exp) *|  
|LTRIM * (string_exp) *||  
|重複 * (string_exp、計數) *|複寫 * (string_exp、計數) *|  
|取代 * (string_exp1、string_exp2 string_exp3) *|STRTRAN * (string_exp1、string_exp2、string_exp3) *|  
|RIGHT * (string_exp，count) *||  
|RTRIM * (string_exp) *||  
|SOUNDEX * (string_exp) *||  
|空間 * (計數) *||  
|子字串 * (string_exp、開始、長度) *|SUBSTR * (string_exp、開始、長度) *|  
|UCASE * (string_exp) *|高 * (string_exp) *|
