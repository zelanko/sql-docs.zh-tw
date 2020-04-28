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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f3ff800938574bec81e9cbb86839e014085a2a8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283850"
---
# <a name="between-predicate"></a>BETWEEN 述詞
語法：  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 只有當*運算式*值大於或等於*運算式*2，且*運算式*2 小於或等於*expression3*時，才會傳回 true。  
  
 對於桌面資料庫驅動程式和 Microsoft Jet 引擎而言，此語法的語義不同。 在 Microsoft Jet SQL 中，*運算式*2 可以大於*expression3* ，如此一來，只有當*運算式*值大於或等於*expression3*，且*運算式*2 小於或等於*運算式*2 時，語句才會傳回 TRUE。
