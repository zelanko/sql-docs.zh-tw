---
title: API 功能的線程安全說明(Oracle 的 ODBC 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 489f0e99ea53d419ff94dddfeb22e37573abb874
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303069"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 函式的執行緒安全性注意事項 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 Oracle 的 Microsoft ODBC 驅動程式是線程安全的;但是,Oracle 不允許在單個連接上有多個併發語句。 驅動程式強制執行此限制。 換句話說,在多線程應用程式中,儘管任何線程可以隨時調用 Oracle 的 ODBC 驅動程式,但驅動程式會阻止來自同一連接上的驅動程式的任何其他線程,直到原始線程離開驅動程式。  
  
 如果兩個不同的連接上有兩個語句,則驅動程式不會阻止。 但是,如果與兩個語句存在單個連接,則存在阻止的可能性。
