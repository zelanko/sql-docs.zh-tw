---
title: 內容連線
description: 描述內容連線。
ms.date: 08/15/2019
ms.assetid: e443ca86-9243-4234-a822-ed10a53a9de0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 40f2c13ddbcdde10b1b406cf23f182e428704242
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247843"
---
# <a name="the-context-connection"></a>內容連線

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

內部資料存取的問題是很常見的案例。 也就是說，您想要存取執行 Commn Language Runtime (CLR) 預存程序或函數所在的同一部伺服器。 有一個選擇是使用 <xref:Microsoft.Data.SqlClient.SqlConnection> 建立連接，指定指向本機伺服器的連接字串，並開啟連接。 這需要指定認證以進行登入。 連接與預存程序或函數位於不同的資料庫工作階段中，因此可能會具有不同的 `SET` 選項、位於單獨交易中，或是找不到暫存資料表等。 如果 Managed 預存程序或函數程式碼是在 SQL Server 處理序中執行的，則會是因為其他使用者已連接至該伺服器並執行 SQL 陳述式來叫用它。 您可能會想讓預存程序或函數在該連接的內容及其交易、`SET` 選項等條件中執行。 這就稱為內容連接。  
  
內容連接可讓您在第一次叫用程式碼的同一內容中執行 Transact-SQL 陳述式。 如需更多詳細資訊，請參閱《SQL Server 線上業書》的[內容連線](https://go.microsoft.com/fwlink/?LinkId=115395)。
