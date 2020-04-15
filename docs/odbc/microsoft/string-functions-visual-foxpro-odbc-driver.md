---
title: 字串功能(可視化福克斯Pro ODBC驅動程式) |微軟文件
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
ms.openlocfilehash: 988ba23b95f6b138148b1fa17ad303d7aa2dc895
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299188"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>字串函式 (Visual FoxPro ODBC Driver)
下表列出了 Visual FoxPro ODBC 驅動程式支援的 ODBC 字串操作功能;當相同函數的 Visual FoxPro 語法與 ODBC 語法不同時,將列出 Visual FoxPro 等效項。  
  
|ODBC 語法|視覺化 FoxPro 語法|  
|------------------|---------------------------|  
|*ASCII (string_exp)*|ASC *(string_exp)*|  
|*CHAR(代碼)*|人權專員 *(string_exp)*|  
|*CONCAT(string_exp1,string_exp2)*|*string_exp1 + string_exp2*|  
|差異 *(string_exp1、string_exp2)*||  
|插入 *(string_exp1、啟動、長度、string_exp2)*|資料 *(string_exp1、開始、長度、string_exp2)*|  
|LCASE *(string_exp)*|下*部(string_exp)*|  
|左 *(string_exp,計數)*||  
|長度 *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|重*覆 (string_exp,計數)*|複製 *(string_exp,計數)*|  
|更換 *(string_exp1、string_exp2、string_exp3)*|斯特朗 *(string_exp1、string_exp2、string_exp3)*|  
|右側 *(string_exp、計數)*||  
|RTRIM *(string_exp)*||  
|音效EX *(string_exp)*||  
|空間 *(計數)*||  
|*SUBSTRING(string_exp、開始、長度)*|*SUBSTR(string_exp、開始、長度)*|  
|UCASE *(string_exp)*|上*部(string_exp)*|
