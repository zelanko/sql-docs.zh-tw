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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139018"
---
# <a name="header-record"></a>標頭記錄
標頭記錄中的欄位包含函式執行的一般資訊，包括傳回碼、資料列計數、狀態記錄的數目，以及執行的語句類型。 除非函數傳回 SQL_INVALID_HANDLE，否則一律會建立標頭記錄。 如需標頭記錄中的完整欄位清單，請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函數描述。
