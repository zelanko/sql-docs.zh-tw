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
ms.openlocfilehash: 7f5fe5cf6aae0d5953cc82b845396dd4164c7fa3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139018"
---
# <a name="header-record"></a>標頭記錄
標頭記錄中的欄位包含函式的執行，包括傳回碼、 資料列計數、 狀態記錄的數目和執行陳述式的型別相關的一般資訊。 除非函式會傳回 SQL_INVALID_HANDLE，一律會建立標頭記錄。 如需標頭記錄中欄位的完整清單，請參閱 < [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函式描述。
