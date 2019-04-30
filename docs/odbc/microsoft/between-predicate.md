---
title: BETWEEN 述詞 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4411345d790e64ae9fb21144a7d82ffe4cd45e8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301963"
---
# <a name="between-predicate"></a>BETWEEN 述詞
語法：  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 傳回，則為 true 才*expression1*大於或等於*expression2*並*expression1*小於或等於*expression3*.  
  
 此語法的語意為桌面資料庫驅動程式和 Microsoft Jet 引擎不同。 在 Microsoft Jet SQL 中， *expression2*可能會大於*expression3*使陳述式會傳回 TRUE，只有當*expression1*大於或等於*expression3*，並*expression1*小於或等於*expression2*。
