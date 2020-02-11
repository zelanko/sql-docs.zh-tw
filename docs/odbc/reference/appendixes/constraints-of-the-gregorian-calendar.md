---
title: 西曆的條件約束 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Gregorian calendar
- Gregorian calendar [ODBC]
ms.assetid: 70667410-c582-4369-8e06-9d98e21cd2bf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f67d313f5a1261dba1f88e9ef3a70d30c1cd503
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019182"
---
# <a name="constraints-of-the-gregorian-calendar"></a>西曆條件約束
日期和日期時間資料類型，以及間隔資料類型的尾端欄位必須符合西曆的條件約束。 這些條件約束如下所示：  
  
-   [Month] 欄位的值必須介於1到12（含）之間。  
  
-   [日] 欄位的值必須在1到當月的天數範圍內。 該月份的天數取決於 [年] 和 [月] 欄位的值，而且可以是28、29、30或31。 （月份中的天數也可以取決於是否為閏年）。  
  
-   [小時] 欄位的值必須介於0到23（含）之間。  
  
-   分鐘欄位的值必須介於0到59（含）之間。  
  
-   針對間隔資料類型的尾端秒欄位，[秒] 欄位的值必須介於0到59.9 （*n*）（含）之間，其中*n*是小數秒數精確度的位數。  
  
-   針對 datetime 資料類型的尾端秒欄位，[秒數] 欄位的值必須介於0到61.9 （*n*）（含）之間，其中*n*指定 "9" 數位的數位，而*n*的值是小數秒有效位數。 （秒的範圍最多允許兩個閏秒，以維持恒星時間的同步處理）。
