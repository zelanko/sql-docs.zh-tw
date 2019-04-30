---
title: 西曆條件約束 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 30fbdd17e7ec5eb970948e1c7133020081222614
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224559"
---
# <a name="constraints-of-the-gregorian-calendar"></a>西曆條件約束
日期和日期時間資料類型，以及結尾欄位的間隔資料類型，必須符合西曆的條件約束。 這些條件約束如下所示：  
  
-   [月] 欄位的值必須是介於 1 到 12 （含) 之間。  
  
-   日期欄位的值必須是介於 1 到月份的天數範圍內。 月中日數的數目決定從年和月欄位的值，它可以是 28、 29、 30 或 31。 （月份中的日數也取決於它是否為閏年）。  
  
-   [小時] 欄位的值必須是介於 0 到 23 之間 （含） 之間。  
  
-   [分鐘] 欄位的值必須是介於 0 到 59 （含) 之間。  
  
-   間隔資料類型的後端的秒數欄位，如秒欄位的值必須是介於 0 到 59.9 (*n*) (含） 之間，其中*n*是數字的小數秒數有效位數的數目。  
  
-   Datetime 資料型別的尾端的秒數欄位，如秒欄位的值必須是介於 0 到 61.9 (*n*) (含） 之間，其中*n*指定"9"的數字的數目和值*n*小數秒數有效位數。 （秒的範圍可以讓維護恒星時間同步處理多達兩個潤秒）。
