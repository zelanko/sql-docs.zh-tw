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
manager: craigg
ms.openlocfilehash: e00b6907d58cda1708cf61907d3c5ff6bf56edfa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238037"
---
# <a name="driver-manager-error-and-warning-checks"></a>驅動程式管理員錯誤和警告檢查
驅動程式管理員完全或部分實作數個函式，並因此檢查所有或部分的錯誤和警告中這些函式。  
  
-   驅動程式管理員會實作**SQLDataSources**並**SQLDrivers**並檢查是否有所有錯誤和警告中這些函式。  
  
-   驅動程式管理員會檢查驅動程式是否會實作**SQLGetFunctions**。 如果驅動程式不會實作**SQLGetFunctions**，驅動程式管理員實作，並檢查所有錯誤和警告，在其中。  
  
-   部分驅動程式管理員會實作**SQLAllocHandle**， **SQLConnect**， **SQLDriverConnect**， **SQLBrowseConnect**， **SQLFreeHandle**， **SQLGetDiagRec**，以及**SQLGetDiagField**並檢查是否有這些函式中的部分錯誤。 因為同時執行類似的作業，它可能會傳回相同的錯誤，為驅動程式的其中一些函式。 例如，驅動程式管理員] 或 [驅動程式可能會傳回 SQLSTATE IM008 （對話方塊失敗） 如果有無法顯示的 [登入] 對話方塊**SQLDriverConnect**。
