---
description: API 函式的執行緒安全性注意事項 (ODBC Driver for Oracle)
title: API 函式的執行緒安全性注意事項 (ODBC Driver for Oracle) |Microsoft Docs
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
ms.openlocfilehash: 8c7da346832e2682caa02bdbdae91a1133a9cbaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449080"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 函式的執行緒安全性注意事項 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 Microsoft ODBC Driver for Oracle 是安全線程;不過，Oracle 不允許在單一連接上使用多個並行語句。 驅動程式會強制執行這種限制。 換句話說，在多執行緒應用程式中，雖然任何執行緒都可以隨時呼叫 ODBC Driver for Oracle，但驅動程式會封鎖相同連接上來自驅動程式的任何其他執行緒，直到原始執行緒離開驅動程式為止。  
  
 如果兩個不同的連接上有兩個語句，則不會封鎖此驅動程式。 但是，如果有兩個語句的單一連接，則可能會封鎖。
