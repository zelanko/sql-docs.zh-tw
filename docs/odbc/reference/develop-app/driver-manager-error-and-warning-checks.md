---
title: 驅動程式管理員錯誤和警告檢查 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d0b136b9748de1991888abb0c19bc0d2ac65ea0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046976"
---
# <a name="driver-manager-error-and-warning-checks"></a>驅動程式管理員錯誤和警告檢查
驅動程式管理員完全或部分執行一些函式，因此會檢查這些函式中的所有或部分錯誤和警告。  
  
-   驅動程式管理員會執行**SQLDataSources**和**SQLDrivers** ，並檢查這些函數中的所有錯誤和警告。  
  
-   驅動程式管理員會檢查驅動程式是否會執行**SQLGetFunctions**。 如果驅動程式不會執行**SQLGetFunctions**，驅動程式管理員會實作用並檢查其中的所有錯誤和警告。  
  
-   驅動程式管理員會部分執行**SQLAllocHandle**、 **SQLConnect**、 **SQLDriverConnect**、 **SQLBrowseConnect**、 **SQLFreeHandle**、 **SQLGetDiagRec**和**SQLGetDiagField** ，並檢查這些函數中是否有一些錯誤。 因為這兩個函式都會執行類似的作業，所以它可能會針對某些函式的驅動程式傳回相同的錯誤。 例如，如果其中一個無法顯示**SQLDriverConnect**的登入對話方塊，驅動程式管理員或驅動程式可能會傳回 SQLSTATE IM008 （對話失敗）。
