---
title: 測試 ODBC 連接 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02509ddb6a986ebb7796d80aca10c6f18cde6e69
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67939700"
---
# <a name="testing-the-odbc-connection"></a>測試 ODBC 連線
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 針對 Oracle 7.x 和 Oracle8 RDBMS 伺服器的 ODBC 存取進行疑難排解時，可能需要確認已正確安裝基礎 SQL * Net 和 Oracle 通訊協定介面卡。 若要這麼做，請使用 Orawin\Bin 目錄中的 Oracle 提供的公用程式 Nettest。  
  
 Nettest 是一個簡單的公用程式，只會使用屬於 Oracle 用戶端的已安裝 SQL * Net 軟體，嘗試登入選取的伺服器。 公用程式會要求登入名稱、密碼和 TNS 連接字串。 如果已正確安裝 Oracle 用戶端，公用程式只會顯示「Ping 成功」。 如果登入失敗，您就必須洽詢資料庫管理員。
