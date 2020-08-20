---
description: 驅動程式的角色
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: afd8f058b12b30140bb193ded7a23e8daf365865
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465644"
---
# <a name="role-of-the-driver"></a>驅動程式的角色
驅動程式會檢查驅動程式管理員未檢查的所有錯誤和警告，以及它所產生的訂單狀態記錄。  (ODBC 2。*x* 驅動程式不會排序狀態記錄。 ) 這包括資料截斷、資料轉換、語法和某些狀態轉換的錯誤和警告。 驅動程式也可能會檢查驅動程式管理員部分檢查的錯誤和警告。 例如，雖然驅動程式管理員會檢查**SQLSetPos** *中的*作業值是否合法，驅動程式還是必須檢查是否受支援。  
  
 驅動程式也會將 *原生錯誤* （也就是資料來源所傳回的錯誤）對應至 SQLSTATEs。 例如，驅動程式可能會將不合法 SQL 語法的許多不同原生錯誤對應到 SQLSTATE 42000 (語法錯誤或存取違規) 。 驅動程式會在狀態記錄的 [SQL_DIAG_NATIVE] 欄位中傳回原生錯誤號碼。 驅動程式檔應該會顯示錯誤和警告如何從資料來源對應到 **SQLGetDiagRec** 和 **SQLGetDiagField**中的引數。
