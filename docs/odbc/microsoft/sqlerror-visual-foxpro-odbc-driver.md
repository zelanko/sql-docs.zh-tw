---
title: SQLError (Visual FoxPro ODBC Driver) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 3014c5c2af1a0ef8e5f485c790089e4807834446
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313283"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：完整  
  
 ODBC API 相容性：核心層級  
  
 傳回最後一個錯誤的錯誤或狀態資訊。 驅動程式會維護的堆疊或可針對傳回的錯誤清單*hstmt*， *hdbc*，並*henv*引數，視呼叫**SQLError**為止。 錯誤佇列中排清每個陳述式之後。  
  
 下表描述**SQLError**引數和驅動程式所使用的傳回值。  
  
|SQLError 引數|傳回值的描述|  
|-----------------------|------------------------------|  
|*szSQLState*|表示錯誤的 SQLSTATE 值。|  
|*pfNativeError*|非零值表示[Visual FoxPro ODBC Driver 原生錯誤訊息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。 值為零表示已偵測到的驅動程式並對應至適當的錯誤[ODBC 錯誤碼](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。|  
|*szErrorMsg*|原生錯誤或 ODBC 錯誤文字。|  
|*pcbErrorMsg*|訊息文字加上之識別項長度的長度。|  
  
 如需有關驅動程式錯誤訊息的詳細資訊，請參閱[錯誤訊息概觀](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)。 如需有關這個函式的詳細資訊，請參閱 < [SQLError](../../odbc/reference/syntax/sqlerror-function.md)中*ODBC 程式設計人員參考*。
