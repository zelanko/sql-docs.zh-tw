---
title: 標頭記錄 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7b6ffacb618dd2b7714be59814f3f1a88a52228
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813916"
---
# <a name="header-record"></a>標頭記錄
標頭記錄中的欄位包含函式的執行，包括傳回碼、 資料列計數、 狀態記錄的數目和執行陳述式的型別相關的一般資訊。 除非函式會傳回 SQL_INVALID_HANDLE，一律會建立標頭記錄。 如需標頭記錄中欄位的完整清單，請參閱 < [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函式描述。
