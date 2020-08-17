---
description: 西曆條件約束
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e473c090a889d54de5ca63bd10b07b410936223f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339364"
---
# <a name="constraints-of-the-gregorian-calendar"></a>西曆條件約束
日期和日期時間資料類型，以及 interval 資料類型的尾端欄位必須符合西曆的條件約束。 這些條件約束如下所示：  
  
-   [月份] 欄位的值必須介於1到12（含）之間。  
  
-   Day 欄位的值必須在1到當月的天數範圍內。 月份中的天數取決於 [年] 和 [月] 欄位的值，而且可以是28、29、30或31。  (月份中的天數也可能取決於是否為閏年。 )   
  
-   [小時] 欄位的值必須介於0到23（含）之間。  
  
-   [分鐘] 欄位的值必須介於0到59（含）之間。  
  
-   若為間隔資料類型的尾端秒欄位，[秒] 欄位的值必須介於0到 59.9 (*n*) （含）之間，其中 *n* 是小數秒精確度的位數。  
  
-   若為 datetime 資料類型的尾端秒欄位，[秒] 欄位的值必須介於0到 61.9 (*n*) （含）之間，其中 *n* 指定 "9" 位數的數位，而 *n* 的值為小數秒精確度。  (的秒數允許最多兩個閏秒的時間，以維護恒星時間的同步處理。 ) 
