---
title: "驅動程式管理員錯誤和警告檢查 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce87b9dbed8cfa6ca621cb72c36220c13ecb0929
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager-error-and-warning-checks"></a>驅動程式管理員錯誤和警告檢查
驅動程式管理員完全或部分實作數個函數，並因此檢查所有或部分的錯誤和警告，這些函式中。  
  
-   驅動程式管理員實作**SQLDataSources**和**SQLDrivers**並檢查是否有所有錯誤和警告，在這些函式。  
  
-   驅動程式管理員會檢查驅動程式是否會實作**SQLGetFunctions**。 如果驅動程式不會實作**SQLGetFunctions**，驅動程式管理員實作，並檢查所有錯誤和警告中的。  
  
-   部分驅動程式管理員會實作**SQLAllocHandle**， **SQLConnect**， **SQLDriverConnect**， **SQLBrowseConnect**， **SQLFreeHandle**， **SQLGetDiagRec**，和**SQLGetDiagField**並檢查是否有這些函式中的部分錯誤。 它可能會傳回相同的錯誤，為驅動程式的其中一些函式，因為同時執行類似作業。 例如，驅動程式管理員或驅動程式可能會傳回 SQLSTATE IM008 （失敗對話方塊） 如果有無法顯示登入 對話方塊的**SQLDriverConnect**。

