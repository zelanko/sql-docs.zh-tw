---
description: 驅動程式管理員的角色
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f974fe6436173b55f39aced45cc38312221cffaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465655"
---
# <a name="role-of-the-driver-manager"></a>驅動程式管理員的角色
驅動程式管理員會決定傳回其產生之狀態記錄的最終順序。 尤其是，它會判斷哪一個記錄具有最高的順位，而且會先傳回。 驅動程式會負責排序其產生的狀態記錄。 如果狀態記錄是由驅動程式管理員和驅動程式所張貼，驅動程式管理員會負責排序它們。 如需詳細資訊，請參閱 [狀態記錄的順序](../../../odbc/reference/develop-app/sequence-of-status-records.md)。  
  
 驅動程式管理員會盡可能地進行錯誤檢查。 這可讓每個驅動程式都檢查相同的錯誤。 例如，如果函式引數接受離散數目的值，例如**SQLSetPos**中*的*作業，驅動程式管理員會檢查指定的值是否合法。  
  
 下列各節說明驅動程式管理員所檢查的條件類型。 這些都不是完整的，如需驅動程式管理員傳回之 SQLSTATEs 的完整清單，請參閱每個函式的「診斷」區段。驅動程式管理員所做的每項檢查的描述都會以「 (DM) 」字母開頭。 另請參閱 [附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)中的狀態轉換表;驅動程式管理員會偵測到括弧中顯示的錯誤。  
  
 此章節包含下列主題。  
  
-   [引數值檢查](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [狀態轉換檢查](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [一般錯誤檢查](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [驅動程式管理員錯誤和警告檢查](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
