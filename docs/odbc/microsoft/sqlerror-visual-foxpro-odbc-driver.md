---
description: SQLError (Visual FoxPro ODBC Driver)
title: SQLError (Visual FoxPro ODBC 驅動程式) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09f901b72d292f962076bff2aa521c8214e8f0e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340254"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：核心層級  
  
 傳回有關最後一個錯誤的錯誤或狀態資訊。 驅動程式會維護可針對 *hstmt*、 *hdbc*和 *henv* 引數傳回的堆疊或錯誤清單，取決於如何進行 **SQLError** 的呼叫。 錯誤佇列會在每個語句之後清除。  
  
 下表描述驅動程式所使用的 **SQLError** 引數和傳回值。  
  
|SQLError 引數|傳回值描述|  
|-----------------------|------------------------------|  
|*szSQLState*|錯誤所代表之 SQLSTATE 的值。|  
|*pfNativeError*|非零值表示 [Visual FOXPRO ODBC 驅動程式原生錯誤訊息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。 值為零表示驅動程式偵測到錯誤，並且對應至適當的 [ODBC 錯誤碼](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。|  
|*szErrorMsg*|原生錯誤或 ODBC 錯誤的文字。|  
|*pcbErrorMsg*|郵件內文的長度加上識別碼的長度。|  
  
 如需驅動程式錯誤訊息的詳細資訊，請參閱 [錯誤訊息總覽](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)。 如需此函數的詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLError](../../odbc/reference/syntax/sqlerror-function.md) 。
