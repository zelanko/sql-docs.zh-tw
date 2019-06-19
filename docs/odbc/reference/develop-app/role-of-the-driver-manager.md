---
title: 驅動程式管理員的角色 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 485cd951992ed427461e497c53d17a4f6db24a38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127245"
---
# <a name="role-of-the-driver-manager"></a>驅動程式管理員的角色
驅動程式管理員會決定最終的順序，在其中傳回它所產生的狀態記錄。 特別是，它會判斷哪一筆記錄具有最高的等級，而是會傳回第一次。 驅動程式會負責排序它所產生的狀態記錄。 如果狀態記錄所公佈的驅動程式管理員和驅動程式，就有一個驅動程式管理員負責來排序它們。 如需詳細資訊，請參閱 <<c0> [ 序號的狀態記錄](../../../odbc/reference/develop-app/sequence-of-status-records.md)。  
  
 驅動程式管理員會盡可能錯誤檢查，因為它可以。 這可讓每個驅動程式檢查有相同的錯誤。 例如，如果函式引數接受離散數目的值，例如*作業*中**SQLSetPos**，驅動程式管理員會檢查指定的值是合法。  
  
 下列各節說明條件檢查驅動程式管理員的類型。 它們並非詳盡資訊;驅動程式管理員會傳回 Sqlstate 的完整清單，請參閱每個函式; 的 「 診斷 」 一節驅動程式管理員所做的每項檢查的描述開頭為字母 」 (DM)。 」 另請參閱中的狀態轉換資料表[附錄 b:ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); 透過驅動程式管理員偵測到錯誤顯示在括弧中。  
  
 此章節包含下列主題。  
  
-   [引數值檢查](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [狀態轉換檢查](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [一般錯誤檢查](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [驅動程式管理員錯誤和警告檢查](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
