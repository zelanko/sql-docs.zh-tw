---
title: "驅動程式管理員的角色 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7718a3d514c6862807cc4b47ecca8729c4c3a162
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="role-of-the-driver-manager"></a>驅動程式管理員的角色
驅動程式管理員會決定最終的順序，以傳回它產生的狀態記錄。 特別是，它會判斷哪一筆記錄具有最高的等級，且會傳回第一次。 驅動程式會負責排序它所產生的狀態記錄。 狀態記錄所公佈的驅動程式管理員和驅動程式，驅動程式管理員會負責排序它們。 如需詳細資訊，請參閱[狀態記錄順序](../../../odbc/reference/develop-app/sequence-of-status-records.md)。  
  
 驅動程式管理員會執行最多錯誤，檢查可能。 這會儲存每個驅動程式檢查有相同的錯誤。 例如，如果函式引數接受離散數目的值，例如*作業*中**SQLSetPos**，驅動程式管理員會檢查指定的值是合法。  
  
 下列章節說明條件檢查驅動程式管理員的類型。 它們不是獨占;驅動程式管理員會傳回 Sqlstate 的完整清單，請參閱 「 診斷 」 區段的每個函式;每個驅動程式管理員所檢查的描述開頭為字母"(DM)。 」 另請參閱中的狀態轉換資料表[附錄 b: ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); 由驅動程式管理員偵測到錯誤顯示在括弧中。  
  
 此章節包含下列主題。  
  
-   [引數值檢查](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [狀態轉換檢查](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [一般錯誤檢查](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [驅動程式管理員錯誤和警告檢查](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
