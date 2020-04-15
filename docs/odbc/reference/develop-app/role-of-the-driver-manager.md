---
title: 驅動程式管理員的角色 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee3d704ea43125c3cd912a4e67d90bf5d50c733e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304299"
---
# <a name="role-of-the-driver-manager"></a>驅動程式管理員的角色
驅動程式管理員確定返回它生成的狀態記錄的最終順序。 特別是,它確定哪個記錄的排名最高,並且要首先返回。 驅動程序負責排序它生成的狀態記錄。 如果狀態記錄由驅動程式管理器和驅動程式發佈,則驅動程式管理器負責排序它們。 有關詳細資訊,請參閱[狀態紀錄序列](../../../odbc/reference/develop-app/sequence-of-status-records.md)。  
  
 驅動程式管理員可以執行盡可能多的錯誤檢查。 這樣,每個驅動程式都免於檢查相同的錯誤。 例如,如果函數參數接受離散數的值(如**SQLSetPos**中的*操作*),驅動程式管理員將檢查指定值是否合法。  
  
 以下各節介紹驅動程式管理器檢查的條件類型。 它們並非詳盡無遺;有關驅動程式管理員返回的 SQLSTATA 的完整清單,請參閱每個函數的「診斷」部分;駕駛員管理員所做的每個檢查的描述以字母"(DM)"開頭。 另請參閱附錄 B 中的狀態轉換[表:ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md);驅動器管理器檢測到括弧中顯示的錯誤。  
  
 此章節包含下列主題。  
  
-   [引數值檢查](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [狀態轉換檢查](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [一般錯誤檢查](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [驅動程式管理員錯誤和警告檢查](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
