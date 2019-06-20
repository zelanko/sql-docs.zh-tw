---
title: API 函式 (ODBC Driver for Oracle) 上的執行緒安全性注意事項 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d1faa7dfd8873b8c11cda5cb3e67d5408c35474
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633213"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 函式的執行緒安全性注意事項 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 Microsoft ODBC Driver for Oracle 是安全執行緒，不過，Oracle 不允許在單一連接上多個並行的陳述式。 驅動程式會強制執行這項限制。 換句話說，在多執行緒應用程式中，雖然任何執行緒可以隨時呼叫 ODBC Driver for Oracle 驅動程式會封鎖在相同連接上的驅動程式的任何其他執行緒直到原始執行緒離開驅動程式。  
  
 如果有兩個陳述式在兩個不同的連接上的驅動程式不會封鎖。 不過，如果沒有與兩個陳述式的單一連線，還有潛在的封鎖。
