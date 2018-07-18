---
title: 程序呼叫逸出序列 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5279794a7f18df2ce2d56210e3ab1373af5cde7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908623"
---
# <a name="procedure-call-escape-sequence"></a>程序呼叫逸出序列
ODBC 使用逸出序列的程序呼叫。 此逸出序列語法如下所示：  
  
 **{**[？ =]**呼叫***程序名稱*[**(**[*參數*] [，[*參數*]]...**)**]**}**  
  
 在 BNF 標記法，語法如下所示：  
  
 *ODBC 的程序逸出*:: =  
  
 &#124;*起始 esc ODBC 端*[？ =] 呼叫*程序 ODBC esc 結束字元*  
  
 *程序*:: =*程序名稱* &#124; *程序名稱*(*程序參數清單*)  
  
 *程序識別項*:: =*使用者定義名稱*  
  
 *程序名稱*:: =*程序識別項*  
  
 &#124;*擁有者名稱*。*程序識別項*  
  
 &#124;*目錄名稱的目錄分隔符號**程序識別項*  
  
 &#124;*目錄名稱的目錄分隔符號*[*擁有者名稱*]。*程序識別項*  
  
 （第三個語法是資料來源不支援的擁有者時才有效）。  
  
 *擁有者名稱*:: =*使用者定義名稱*  
  
 *目錄名稱*:: =*使用者定義名稱*  
  
 *目錄分隔符號*:: = {*實作定義*}  
  
 (目錄分隔符號透過傳回**SQLGetInfo** SQL_CATALOG_NAME_SEPARATOR 資訊選項。)  
  
 *程序參數清單*:: =*程序參數*  
  
 &#124;*程序參數*，*程序參數清單*  
  
 *程序參數*:: =*動態參數* &#124; *常值* &#124; *空白字串*  
  
 *空白字串*:: =  
  
 *起始 esc ODBC 端*:: = {  
  
 *ODBC esc 結束字元*:: =}  
  
 （如果程序參數為空字串，程序會使用預設值為該參數。）  
  
 若要判斷資料來源支援程序及驅動程式支援 ODBC 的程序引動過程語法，應用程式可以呼叫**SQLGetInfo** SQL_PROCEDURES 資訊類型。
