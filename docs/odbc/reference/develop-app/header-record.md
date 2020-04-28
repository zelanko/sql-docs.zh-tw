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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 372185966cc1644147feb2683177ae3a5b69e788
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300178"
---
# <a name="header-record"></a>標頭記錄
標頭記錄中的欄位包含函式執行的一般資訊，包括傳回碼、資料列計數、狀態記錄的數目，以及執行的語句類型。 除非函數傳回 SQL_INVALID_HANDLE，否則一律會建立標頭記錄。 如需標頭記錄中的完整欄位清單，請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函數描述。
