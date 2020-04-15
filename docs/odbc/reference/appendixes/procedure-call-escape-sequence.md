---
title: 過程呼叫轉義序列 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298218"
---
# <a name="procedure-call-escape-sequence"></a>程序呼叫逸出序列
ODBC 使用轉義序列進行過程呼叫。 此逸出序列的語法如下:  
  
 **【****%***procedure-name*11 >**(***parameter**parameter***)**]**}**  
  
 在 BNF 符號中,語法如下所示:  
  
 *ODBC-程式轉義*::*  
  
 &#124; *ODBC-esc -發款器*[? ] 呼叫*程式 ODBC-esc 終止器*  
  
 *過程*::**過程名稱*&#124;*過程名稱*(*過程參數清單*)  
  
 *行程識別碼*::**使用者定義的名稱*  
  
 *過程名稱*::**程序識別碼*  
  
 &#124;*擁有者名稱*。*程序識別碼*  
  
 &#124;*目錄名稱目錄分隔符**程序識別碼*  
  
 &#124;*目錄名稱目錄分隔符*=*擁有者名稱*[擁有者名稱]。*程序識別碼*  
  
 (僅當數據源不支援所有者時,第三個語法才有效。  
  
 *擁有者名稱*::**使用者定義名稱*  
  
 *目錄名稱*::**使用者定義名稱*  
  
 *目錄分離器*::* =*實現定義*|  
  
 (目錄分隔符通過**SQLGetInfo**傳回,並帶有SQL_CATALOG_NAME_SEPARATOR資訊選項。  
  
 *錯誤參數清單*::**過程參數*  
  
 &#124;*時可以檢查 ,**過程參數清單*  
  
 *錯誤參數*::**動態參數*&#124;*文字*&#124;*空字串*  
  
 *空字串*::*  
  
 *ODBC-esc -發物人*::*  
  
 *ODBC-esc 終結器*:*|  
  
 (如果過程參數為空字串,則該過程使用該參數的默認值。  
  
 要確定資料來源是否支援程序,驅動程式是否支援 ODBC 過程呼叫語法,應用程式可以使用SQL_PROCEDURES資訊類型呼叫**SQLGetInfo。**
