---
title: 錯誤訊息（Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286398"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>錯誤訊息 (Visual FoxPro ODBC Driver)
當錯誤發生時，Visual FoxPro 驅動程式會傳回下列資訊：  
  
-   原生錯誤號碼和錯誤訊息正文  
  
-   SQLSTATE （ODBC 錯誤碼）和錯誤訊息正文  
  
 您可以藉由呼叫[SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)來存取此錯誤資訊。  
  
## <a name="native-errors"></a>原生錯誤  
 對於資料來源中發生的錯誤，Visual FoxPro 驅動程式會傳回原生錯誤號碼和錯誤訊息正文。 如需原生錯誤號碼的清單，請參閱[Visual FOXPRO ODBC Driver 原生錯誤訊息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC 錯誤碼)  
 對於 Visual FoxPro 驅動程式偵測到並傳回的錯誤，驅動程式會將傳回的原生錯誤號碼對應至適當的 SQLSTATE。 如果原生錯誤號碼沒有要對應的 ODBC 錯誤碼，Visual FoxPro 驅動程式會傳回 SQLSTATE S1000 （一般錯誤）。  
  
 如需 Visual FoxPro ODBC 驅動程式針對對應的 Visual FoxPro 錯誤所產生的 SQLSTATE 值清單，請參閱[ODBC 錯誤碼](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。  
  
## <a name="syntax"></a>語法  
 錯誤訊息的格式如下：  
  
 **[** *廠商* **] [** *ODBC_component* **]** *error_message*  
  
 以方括弧（[]）括住的前置詞，可識別下表所定義的錯誤來源。  
  
|資料來源|前置詞|值|  
|-----------------|------------|-----------|  
|驅動程式管理員|製造商<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 驅動程式管理員]<br />N/A|  
|Visual FoxPro 驅動程式|製造商<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC Visual FoxPro 驅動程式]<br />N/A|  
  
 例如，如果 Visual FoxPro ODBC 驅動程式找不到檔案 employee，它可能會傳回下列錯誤訊息：  
  
 "[*Microsoft*] [*ODBC Visual FoxPro Driver*] 檔案 ' employee .dbf ' 不存在」
