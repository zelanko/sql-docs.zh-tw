---
title: 程序呼叫 Escape 順序 |Microsoft Docs
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
ms.openlocfilehash: 1194efe6a21c456a722ccd4352661c998f0316d9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298218"
---
# <a name="procedure-call-escape-sequence"></a>程序呼叫逸出序列
ODBC 會使用逸出序列進行程序呼叫。 此 escape 序列的語法如下：  
  
 **{**[？ =]**呼叫***程式名稱*[**（**[*參數*] [，[*參數*]] .。。**)**]**}**  
  
 在 BNF 標記法中，語法如下所示：  
  
 *ODBC-程式-escape* ：： =  
  
 &#124; *ODBC-esc-啟動器*[？ =] 呼叫程式*ODBC-esc-結束字元*  
  
 *procedure* ：： = 程式*名稱*&#124;*程式名稱*（*程式-參數清單*）  
  
 程式*識別碼*：： =*使用者定義名稱*  
  
 *程式名稱*：： =*程式-識別碼*  
  
 &#124;*擁有者名稱*。*程式識別碼*  
  
 &#124;*目錄-名稱目錄-分隔符號*程式 *-識別碼*  
  
 &#124;*目錄-名稱目錄-分隔符號*[*擁有者名稱*]。*程式識別碼*  
  
 （只有在資料來源不支援擁有者時，第三個語法才有效）。  
  
 *owner-name* ：： =*使用者定義名稱*  
  
 *catalog-name* ：： =*使用者定義名稱*  
  
 *catalog-separator* ：： = {*執行定義的*}  
  
 （使用 SQL_CATALOG_NAME_SEPARATOR 資訊選項，透過**SQLGetInfo**傳回目錄分隔符號）。  
  
 *程式-參數清單*：： = 程式 *-參數*  
  
 &#124; 程式*參數*、程式*參數清單*  
  
 *程式參數*：： =*動態參數*&#124;*常*值 &#124;*空字串*  
  
 *空字串*：： =  
  
 *ODBC-esc-啟動器*：： = {  
  
 *ODBC-esc-結束字元*：： =}  
  
 （如果程式參數是空字串，程式會使用該參數的預設值）。  
  
 若要判斷資料來源是否支援程式，而且該驅動程式支援 ODBC 程序呼叫語法，應用程式可以使用 SQL_PROCEDURES 資訊類型來呼叫**SQLGetInfo** 。
