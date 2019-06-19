---
title: 錯誤訊息 (Visual FoxPro ODBC Driver) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b24db48d6a76c221e72944e8e5e6826cb8d5d55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127981"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>錯誤訊息 (Visual FoxPro ODBC Driver)
發生錯誤時，Visual FoxPro 驅動程式會傳回下列資訊：  
  
-   原生錯誤號碼和錯誤訊息文字  
  
-   SQLSTATE （ODBC 錯誤碼） 和錯誤訊息文字  
  
 您藉由呼叫來存取此錯誤資訊[SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)。  
  
## <a name="native-errors"></a>原生錯誤  
 在 資料來源中發生的錯誤，Visual FoxPro 驅動程式會傳回自發性錯誤號碼和錯誤訊息文字。 如需原生錯誤碼的清單，請參閱 < [Visual FoxPro ODBC Driver 原生錯誤訊息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC 錯誤碼)  
 已偵測到並 Visual FoxPro 驅動程式所傳回的錯誤，驅動程式會將傳回的自發性錯誤號碼對應到適當的 SQLSTATE。 如果自發性錯誤號碼沒有要對應至 ODBC 錯誤碼，Visual FoxPro 驅動程式會傳回 SQLSTATE S1000 （一般錯誤）。  
  
 如需 Visual FoxPro ODBC Driver for Visual FoxPro 的相對應錯誤所產生的 SQLSTATE 值的清單，請參閱 < [ODBC 錯誤碼](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。  
  
## <a name="syntax"></a>語法  
 錯誤訊息的格式如下：  
  
 **[** *vendor* **][** *ODBC_component* **]** *error_message*  
  
 下表中所定義，在括號 ([]) 中的前置詞會識別錯誤的來源。  
  
|資料來源|Prefix|值|  
|-----------------|------------|-----------|  
|驅動程式管理員|[vendor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 驅動程式管理員]<br />N/A|  
|Visual FoxPro 驅動程式|廠商]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC Visual FoxPro 驅動程式]<br />N/A|  
  
 例如，如果 Visual FoxPro ODBC Driver 找不到檔案 employee.dbf，它可能會傳回下列錯誤訊息：  
  
 "[*Microsoft*] [*ODBC Visual FoxPro Driver*] 檔案 'employee.dbf' 不存在 」
