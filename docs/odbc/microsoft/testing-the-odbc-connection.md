---
description: 測試 ODBC 連線
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61a471af3c5681ca58ca3268ad4512ee80abb9cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421542"
---
# <a name="testing-the-odbc-connection"></a>測試 ODBC 連線
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 針對 Oracle 7.x 和 Oracle8 RDBMS 伺服器的 ODBC 存取進行疑難排解時，可能需要確認是否已正確安裝基礎 SQL * Net 和 Oracle 通訊協定介面卡。 若要這樣做，請使用 Orawin\Bin 目錄中的 Oracle 提供的公用程式 Nettest.exe。  
  
 Nettest 是一個簡單的公用程式，它只會嘗試使用屬於 Oracle 用戶端的已安裝 SQL * Net 軟體登入選取的伺服器。 公用程式會要求登入名稱、密碼和 TNS 連接字串。 如果已正確安裝 Oracle 用戶端，公用程式就只會顯示「Ping 成功」。 如果登入失敗，您將需要洽詢資料庫管理員。
