---
title: 測試 ODBC 連線 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8de19af2b50a58eef22ec074a308f86717278a48
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303109"
---
# <a name="testing-the-odbc-connection"></a>測試 ODBC 連線
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 在排除對 Oracle 7.x 和 Oracle8 RDBMS 伺服器的 ODBC 存取進行故障排除時,可能需要驗證基礎 SQL_Net和 Oracle 協定適配器是否已正確安裝。 為此,請使用Orawin_Bin目錄中的 Oracle 提供的實用程式 Nettest.exe。  
  
 Nettest 是一個簡單的實用程式,它嘗試僅使用作為 Oracle 用戶端一部分的已安裝的 SQL_Net 軟體登錄到選定的伺服器。 該實用程式將要求一個登錄名、密碼和 TNS 連接字串。 如果 Oracle 用戶端安裝正確,實用程式將僅顯示「Ping 成功」。 如果登錄不成功,則需要諮詢資料庫管理員。
