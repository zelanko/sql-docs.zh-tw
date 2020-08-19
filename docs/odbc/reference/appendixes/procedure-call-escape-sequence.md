---
description: 程序呼叫逸出序列
title: 程序呼叫 Escape 序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba88f3d78edeaa1ce4f4884977656cd8a4a16062
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483221"
---
# <a name="procedure-call-escape-sequence"></a>程序呼叫逸出序列
ODBC 使用轉義順序進行程序呼叫。 此 escape 順序的語法如下所示：  
  
 **{**[？ =]**呼叫***程式-名稱*[** (**[*參數*] [，[*參數*]] .。。**) **]**}**  
  
 在 BNF 標記法中，語法如下所示：  
  
 *ODBC-procedure-escape* ：： =  
  
 &#124; *ODBC-esc-啟動器* [？ =] CALL *procedure ODBC-esc-結束字元*  
  
 *procedure* ：： = *程式名稱* &#124; *程式-名稱* (程式 *-參數清單*)   
  
 *procedure 識別碼* ：： = *使用者定義的名稱*  
  
 *procedure-name* ：： = *程式識別碼*  
  
 &#124; *擁有者名稱*。*程式識別碼*  
  
 &#124; *目錄-名稱目錄-分隔符號*程式 *識別碼*  
  
 &#124; *目錄-名稱目錄-分隔符號* [*擁有者名稱*]。*程式識別碼*  
  
  (第三個語法只有在資料來源不支援擁有者時才有效。 )   
  
 *擁有者名稱* ：： = *使用者定義的名稱*  
  
 *目錄名稱* ：： = *使用者定義的名稱*  
  
 *目錄-分隔符號* ：： = {*實作為定義*}  
  
  (使用 SQL_CATALOG_NAME_SEPARATOR 資訊選項透過 **SQLGetInfo** 傳回類別目錄分隔符號。 )   
  
 *procedure-parameter-list* ：： = *procedure-parameter*  
  
 &#124; *程式-參數*、程式 *-參數-清單*  
  
 *procedure 參數* ：： = *dynamic-參數* &#124; *常* 值 &#124; *空白字串*  
  
 *空字串* ：： =  
  
 *ODBC-esc-啟動器* ：： = {  
  
 *ODBC-esc-結束字元* ：： =}  
  
  (如果 procedure 參數是空字串，程式會使用該參數的預設值。 )   
  
 若要判斷資料來源是否支援程式，以及驅動程式是否支援 ODBC 程序呼叫語法，應用程式可以使用 SQL_PROCEDURES 資訊類型來呼叫 **SQLGetInfo** 。
