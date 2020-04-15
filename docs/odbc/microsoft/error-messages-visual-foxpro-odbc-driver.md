---
title: 錯誤消息(可視化福克斯 Pro ODBC 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31f894e58da93fe6091dba306f8b765d14bac2cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286398"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>錯誤訊息 (Visual FoxPro ODBC Driver)
發生錯誤時,Visual FoxPro 驅動程式傳回以下資訊:  
  
-   這個機錯誤編號與錯誤訊息文字  
  
-   SQLSTATE(ODBC 錯誤代碼)與錯誤訊息文字  
  
 您可以通過呼叫[SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)來存取此錯誤資訊。  
  
## <a name="native-errors"></a>本機錯誤  
 對於資料源中發生的錯誤,Visual FoxPro 驅動程式返回本機錯誤編號和錯誤消息文本。 有關本機錯誤編號的清單,請參閱可視化[FoxPro ODBC 驅動程式本機錯誤訊息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC 錯誤碼)  
 對於 Visual FoxPro 驅動程式檢測到和返回的錯誤,驅動程式將返回的本機錯誤編號映射到相應的 SQLSTATE。 如果本機錯誤編號沒有要映射到的 ODBC 錯誤代碼,則 Visual FoxPro 驅動程式將返回 SQLSTATE S1000(一般錯誤)。  
  
 有關 Visual FoxPro ODBC 驅動程式產生的 SQLSTATE 值清單,請參閱[ODBC 錯誤代碼](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。  
  
## <a name="syntax"></a>語法  
 錯誤訊息具有以下格式:  
  
 **【** *供應商* **】** *ODBC_component* **】** *error_message*  
  
 括號 (* +) 中的前置碼識別下表中定義的錯誤來源。  
  
|資料來源|前置詞|值|  
|-----------------|------------|-----------|  
|驅動程式管理員|[供應商]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 驅動程式管理員]<br />N/A|  
|視覺化福斯專業驅動程式|供應商*<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 視覺福克斯專業驅動程式]<br />N/A|  
  
 例如,如果 Visual FoxPro ODBC 驅動程式找不到檔案員工.dbf,它可能會返回以下錯誤訊息:  
  
 [*微軟*]*ODBC 可視化福克斯Pro驅動程式*[檔 '員工.dbf' 不存在"
