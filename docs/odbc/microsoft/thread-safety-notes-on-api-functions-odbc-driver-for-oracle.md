---
title: "應用程式開發介面函式 （如 Oracle 的 ODBC 驅動程式） 的執行緒安全注意事項 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f8519d900e9cbb4e9c942fdfcccfb21a63d14705
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>執行緒安全附註的 API 函式 （如 Oracle 的 ODBC 驅動程式）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 Microsoft ODBC Driver for Oracle 是安全執行緒，不過，Oracle 不允許在單一連接上多個並行的陳述式。 驅動程式會強制執行這項限制。 換句話說，多執行緒應用程式中，雖然任何執行緒在任何時候，就可以呼叫 ODBC Driver for Oracle 驅動程式會封鎖從相同的連接上的驅動程式的其他任何執行緒直到原始的執行緒離開驅動程式。  
  
 在兩個不同的連接上的兩個陳述式時，驅動程式不會封鎖。 不過，如果沒有兩個陳述式的單一連線，則潛在的封鎖。
