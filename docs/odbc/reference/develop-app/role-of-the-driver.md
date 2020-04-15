---
title: 驅動程式的角色 |微軟文件
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
ms.openlocfilehash: 8c683d990aaa3fd6892369e734c06fd1c356bd0f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304279"
---
# <a name="role-of-the-driver"></a>驅動程式的角色
驅動程式檢查驅動程式管理器未檢查的所有錯誤和警告,並命令它生成的狀態記錄。 (ODBC 2。*x*驅動程式不訂購狀態記錄。這包括數據截斷、數據轉換、語法和某些狀態轉換中的錯誤和警告。 驅動程式還可能檢查驅動程式管理器部分檢查的錯誤和警告。 例如,儘管驅動程式管理器檢查**SQLSetPos***中的操作*值是否合法,但驅動程式必須檢查它是否受支援。  
  
 該驅動程式還將*本機錯誤*(即資料源返回的錯誤)映射到 SQLSTAT。 例如,驅動程式可能會將非法 SQL 語法的許多不同的本機錯誤映射到 SQLSTATE 42000(語法錯誤或訪問衝突)。 驅動程式返回狀態記錄SQL_DIAG_NATIVE欄位中的本機錯誤編號。 驅動程式文件應顯示如何從資料來源映射到**SQLGetDiagRec**和**SQLGetDiagField**中的參數。
