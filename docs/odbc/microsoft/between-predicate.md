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
ms.openlocfilehash: 1a0ac99729966acdcb03c2aab0175c34bba0c08a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138121"
---
# <a name="between-predicate"></a>BETWEEN 述詞
語法：  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 傳回，則為 true 才*expression1*大於或等於*expression2*並*expression1*小於或等於*expression3*.  
  
 此語法的語意為桌面資料庫驅動程式和 Microsoft Jet 引擎不同。 在 Microsoft Jet SQL 中， *expression2*可能會大於*expression3*使陳述式會傳回 TRUE，只有當*expression1*大於或等於*expression3*，並*expression1*小於或等於*expression2*。
