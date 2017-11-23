---
title: "錯誤訊息 （Visual FoxPro ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27a6df2276d2d474137038fdbe0b42fdf2b05e5b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>錯誤訊息 （Visual FoxPro ODBC 驅動程式）
發生錯誤時，Visual FoxPro 驅動程式會傳回下列資訊：  
  
-   原生錯誤號碼和錯誤訊息文字  
  
-   SQLSTATE （ODBC 錯誤碼） 和錯誤訊息文字  
  
 存取此錯誤的資訊，請呼叫[SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)。  
  
## <a name="native-errors"></a>原生錯誤  
 資料來源中發生的錯誤，Visual FoxPro 驅動程式會傳回自發性錯誤號碼和錯誤訊息文字。 如需原生錯誤號碼的清單，請參閱[Visual FoxPro ODBC 驅動程式原生錯誤訊息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC 錯誤碼)  
 已偵測到並 Visual FoxPro 驅動程式傳回的錯誤，此驅動程式會將傳回的自發性錯誤號碼對應至適當的 SQLSTATE。 如果自發性錯誤號碼沒有要對應至 ODBC 錯誤碼，Visual FoxPro 驅動程式會傳回 SQLSTATE S1000 （一般的錯誤）。  
  
 如需對應 Visual FoxPro 錯誤 Visual FoxPro ODBC 驅動程式所產生的 SQLSTATE 值的清單，請參閱[ODBC 錯誤碼](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。  
  
## <a name="syntax"></a>語法  
 錯誤訊息的格式如下：  
  
 **[** *廠商* **] [** *ODBC_component* **]** *error_message*  
  
 下表中所定義，括號 ([]) 中的前置詞會識別錯誤的來源。  
  
|資料來源|前置詞|值|  
|-----------------|------------|-----------|  
|驅動程式管理員|[廠商]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 驅動程式管理員]<br />不適用|  
|Visual FoxPro 驅動程式|廠商]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC Visual FoxPro 驅動程式]<br />不適用|  
  
 例如，如果 Visual FoxPro ODBC 驅動程式找不到檔案 employee.dbf，它可能會傳回下列錯誤訊息：  
  
 "[*Microsoft*] [*ODBC Visual FoxPro 驅動程式*] 'employee.dbf' 不存在 」
