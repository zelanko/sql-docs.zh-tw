---
title: 公曆的約束 |微軟文件
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
ms.openlocfilehash: f88842c7426e17af1fdc0533b8b97e2c559de237
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284758"
---
# <a name="constraints-of-the-gregorian-calendar"></a>西曆條件約束
日期和日期時間數據類型以及間隔數據類型的尾隨欄位必須符合公曆的約束。 這些限制如下:  
  
-   月欄位的值必須介於 1 和 12 之間(包括)。  
  
-   日欄位的值必須在 1 到月份天數的範圍內。 當月中的天數根據年份和月份欄位的值確定,可以為 28、29、30 或 31。 (當月中的天數還取決於它是否是閏年。  
  
-   小時欄位的值必須介於 0 和 23 之間(包括)。  
  
-   分鐘欄位的值必須介於 0 和 59 之間(包括)。  
  
-   對於間隔數據類型的尾隨秒欄位,秒欄位的值必須介於 0 和 59.9(n )*n*之間,其中*n*是小數秒精度中的位數。  
  
-   對於日期時間數據類型的尾隨秒欄位,秒欄位的值必須介於 0 和 61.9(n )*n*之間,其中*n*指定"9"位數 *,n*的值為小數秒精度。 (秒的範圍允許多達兩個閏秒來保持次真時間的同步。
