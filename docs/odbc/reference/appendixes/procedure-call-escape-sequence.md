---
title: 程序呼叫逸出序列 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 914bd4759552680a57c345dc3a7c3bc1bcc103a6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806556"
---
# <a name="procedure-call-escape-sequence"></a>程序呼叫逸出序列
ODBC 會將逸出序列用於程序呼叫。 此逸出序列的語法如下所示：  
  
 **{**[？ =]**呼叫***程序名稱*[**(**[*參數*] [，[*參數*]]...**)**]**}**  
  
 在 backus-naur form，BNF 標記法中，語法如下所示：  
  
 *ODBC 程序逸出*:: =  
  
 &#124;*ODBC-esc-啟動器*[？ =] 呼叫*程序 ODBC esc 鍵結束字元*  
  
 *程序*:: =*程序名稱* &#124; *程序名稱*(*程序參數清單*)  
  
 *程序識別項*:: =*使用者定義名稱*  
  
 *程序名稱*:: =*程序識別項*  
  
 &#124;*擁有者名稱*。*程序識別項*  
  
 &#124;*目錄名稱的目錄分隔符號**程序識別項*  
  
 &#124;*目錄名稱的目錄分隔符號*[*擁有者名稱*]。*程序識別項*  
  
 （第三個的語法是資料來源不支援擁有者時，才有效）。  
  
 *擁有者名稱*:: =*使用者定義名稱*  
  
 *目錄名稱*:: =*使用者定義名稱*  
  
 *目錄分隔符號*:: = {*實作定義*}  
  
 (經由傳回的目錄分隔符號**SQLGetInfo** SQL_CATALOG_NAME_SEPARATOR 資訊選項。)  
  
 *程序參數清單*:: =*程序參數*  
  
 &#124;*程序參數*，*程序參數清單*  
  
 *程序參數*:: =*動態參數* &#124; *常值* &#124; *空字串*  
  
 *空字串*:: =  
  
 *起始 esc ODBC 端*:: = {  
  
 *ODBC esc 鍵結束字元*:: =}  
  
 （程序參數是否為空字串，此程序使用的預設值為該參數。）  
  
 若要判斷資料來源支援程序及驅動程式支援 ODBC 的程序引動過程語法，應用程式可以呼叫**SQLGetInfo** SQL_PROCEDURES 資訊類型。
