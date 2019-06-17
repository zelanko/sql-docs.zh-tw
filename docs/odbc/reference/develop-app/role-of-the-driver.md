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
manager: craigg
ms.openlocfilehash: b940eac1548582285e7d41e0014cfe911dfb1137
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63254185"
---
# <a name="role-of-the-driver"></a>驅動程式的角色
驅動程式會檢查所有錯誤和警告不會檢查驅動程式管理員，並排序它所產生的狀態記錄。 資料庫連接 (ODBC 2。*x*驅動程式不會排序狀態記錄。)這包括錯誤和警告中的資料截斷、 資料轉換、 語法和某些狀態轉換。 錯誤和警告部分核取驅動程式管理員，也可能會檢查驅動程式。 比方說，雖然驅動程式管理員會檢查是否的值*作業*中**SQLSetPos**是合法的此驅動程式必須檢查它是否支援。  
  
 驅動程式也會對應*原生錯誤*-也就是資料來源傳回的錯誤-以 Sqlstate。 例如，驅動程式可能會對應數個不同的不合法的 SQL 語法以 SQLSTATE 42000 （語法錯誤或存取違規） 的原生錯誤。 驅動程式會傳回自發性錯誤號碼在狀態記錄的 SQL_DIAG_NATIVE 欄位中。 驅動程式文件應該會顯示錯誤和警告的對應方式從資料來源中的引數**SQLGetDiagRec**並**SQLGetDiagField**。
