---
title: 驅動程式的角色 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7c344c1d8b3a4702728807af9dae7ed9ca7c5cd0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020378"
---
# <a name="role-of-the-driver"></a>驅動程式的角色
驅動程式會檢查驅動程式管理員未檢查的所有錯誤和警告，並列出其產生的訂單狀態記錄。 （ODBC 2。*x*驅動程式不會對狀態記錄進行排序）。這包括資料截斷、資料轉換、語法和一些狀態轉換中的錯誤和警告。 驅動程式也可能會檢查驅動程式管理員部分檢查的錯誤和警告。 例如，雖然驅動程式管理員會檢查**SQLSetPos**中的*Operation*值是否合法，但驅動程式必須檢查是否受到支援。  
  
 驅動程式也會將*原生錯誤*（也就是資料來源所傳回的錯誤）對應到 SQLSTATEs。 例如，驅動程式可能會將不合法 SQL 語法的一些不同原生錯誤對應至 SQLSTATE 42000 （語法錯誤或存取違規）。 驅動程式會在狀態記錄的 [SQL_DIAG_NATIVE] 欄位中傳回原生錯誤號碼。 驅動程式檔應該會顯示錯誤和警告如何從資料來源對應到**SQLGetDiagRec**和**SQLGetDiagField**中的引數。
