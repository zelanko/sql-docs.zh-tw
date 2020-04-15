---
title: 在謂詞之間 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283850"
---
# <a name="between-predicate"></a>BETWEEN 述詞
語法：  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 僅當*表達式1*大於或等於*表達式2*且*運算式1*小於或等於*表達式3*時,才返回 true。  
  
 對於桌面資料庫驅動程式和Microsoft Jet引擎,此語法的語義是不同的。 Microsoft Jet SQL 中,*表示式 2*可以大於*表示式 3,* 因此僅當*表示式 1*大於或等於*運算式 3*時,運算式 2 才會傳回 TRUE,並且*運算式 1*小於或等於*運算式 2*。
