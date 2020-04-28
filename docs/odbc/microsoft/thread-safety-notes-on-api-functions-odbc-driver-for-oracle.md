---
title: API 函式的執行緒安全性注意事項（ODBC Driver for Oracle） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303069"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 函式的執行緒安全性注意事項 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 Microsoft ODBC Driver for Oracle 是安全線程;不過，Oracle 不允許在單一連接上使用多個並行語句。 驅動程式會強制執行這種限制。 換句話說，在多執行緒應用程式中，雖然任何執行緒都可以隨時呼叫 ODBC Driver for Oracle，驅動程式還是會封鎖相同連接上驅動程式中的任何其他執行緒，直到原始執行緒離開驅動程式為止。  
  
 如果兩個不同的連接上有兩個語句，驅動程式不會封鎖。 不過，如果有兩個語句的單一連接，可能會封鎖。
