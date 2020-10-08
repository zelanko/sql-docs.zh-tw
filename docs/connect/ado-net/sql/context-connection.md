---
title: 內容連線
description: 描述內容連線。
ms.date: 08/15/2019
ms.assetid: e443ca86-9243-4234-a822-ed10a53a9de0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: b8d98dc60d40d40041375370b04c698768d0f324
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725662"
---
# <a name="the-context-connection"></a>內容連線

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

內部資料存取的問題是很常見的案例。 也就是說，您想要存取執行 Commn Language Runtime (CLR) 預存程序或函數所在的同一部伺服器。 有一個選擇是使用 <xref:Microsoft.Data.SqlClient.SqlConnection> 建立連接，指定指向本機伺服器的連接字串，並開啟連接。 這需要指定認證以進行登入。 連接與預存程序或函數位於不同的資料庫工作階段中，因此可能會具有不同的 `SET` 選項、位於單獨交易中，或是找不到暫存資料表等。 如果 Managed 預存程序或函數程式碼是在 SQL Server 處理序中執行的，則會是因為其他使用者已連接至該伺服器並執行 SQL 陳述式來叫用它。 您可能會想讓預存程序或函數在該連接的內容及其交易、`SET` 選項等條件中執行。 這就稱為內容連接。  
  
內容連接可讓您在第一次叫用程式碼的同一內容中執行 Transact-SQL 陳述式。 如需更多詳細資訊，請參閱《SQL Server 線上業書》的[內容連線](/previous-versions/sql/sql-server-2008/ms131053(v=sql.100))。