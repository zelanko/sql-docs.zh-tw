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
manager: craigg
ms.openlocfilehash: 543ab436ac7dca5e0d5965220cd90a798afb5ccf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633173"
---
# <a name="testing-the-odbc-connection"></a>測試 ODBC 連線
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 針對至 Oracle 的 ODBC 存取進行疑難排解時 7.x 和 Oracle8 RDBMS 伺服器，可能需要確認基礎 SQL * Net Oracle 通訊協定配接器已正確安裝。 若要這樣做，請使用 Oracle 提供公用 Nettest.exe Orawin\Bin 目錄中。  
  
 Nettest 是一個簡單的公用程式，嘗試登入到選取的伺服器使用已安裝的 SQL * Net 屬於 Oracle 用戶端的軟體。 公用程式會要求提供登入名稱、 密碼和 TNS 連接字串。 如果已正確安裝 Oracle 用戶端，此公用程式只會顯示 「 Ping 成功。 」 如果登入不成功，您必須洽詢資料庫管理員。
