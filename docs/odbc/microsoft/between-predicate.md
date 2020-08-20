---
description: BETWEEN 述詞
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
ms.openlocfilehash: 2f2283f5824e4be0c9702bfe8feef9fe3109849a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500381"
---
# <a name="between-predicate"></a>BETWEEN 述詞
語法：  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 只有當 *運算式* 值大於或等於 *運算式* 且 *運算式* 值小於或等於 *expression3*時，才會傳回 true。  
  
 這種語法的語法與桌面資料庫驅動程式和 Microsoft Jet 引擎的語法不同。 在 Microsoft Jet SQL 中， *運算式運算式* 可以大於 *expression3* ，如此一來，只有當 *運算式* 值大於或等於 *expression3*，且 *運算式* 值小於或等於 *運算式*時，語句才會傳回 TRUE。
