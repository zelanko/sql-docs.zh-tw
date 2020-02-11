---
title: SQLError （Visual FoxPro ODBC Driver） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLError function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8315ec16-1c22-447a-a577-39bd94f61070
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d7e8a60030e9c5c7666ce3b25488cfc6adf00783
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053861"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：核心層級  
  
 傳回關於最後一個錯誤的錯誤或狀態資訊。 驅動程式會維護可針對*hstmt*、 *hdbc*和*henv*引數傳回的堆疊或錯誤清單，視對**SQLError**的呼叫的方式而定。 錯誤佇列會在每個語句之後清除。  
  
 下表描述驅動程式所使用的**SQLError**引數和傳回值。  
  
|SQLError 引數|傳回值描述|  
|-----------------------|------------------------------|  
|*szSQLState*|錯誤所表示的 SQLSTATE 值。|  
|*pfNativeError*|非零值表示[Visual FOXPRO ODBC Driver 原生錯誤訊息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。 值為零表示驅動程式偵測到錯誤，並對應至適當的[ODBC 錯誤碼](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。|  
|*szErrorMsg*|原生錯誤或 ODBC 錯誤的文字。|  
|*pcbErrorMsg*|郵件內文的長度加上識別碼的長度。|  
  
 如需有關驅動程式錯誤訊息的詳細資訊，請參閱[錯誤訊息總覽](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)。 如需此函數的詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLError](../../odbc/reference/syntax/sqlerror-function.md) 。
