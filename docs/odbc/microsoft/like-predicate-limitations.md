---
title: 喜歡謂詞限制 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d596d688956d7bdbf3d9125184d81c16249781c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298958"
---
# <a name="like-predicate-limitations"></a>LIKE 述詞限制
如果列中的數據長於 255 個字元,則 LIKE 比較將僅基於前 255 個字元。  
  
 過程中使用的 LIKE 僅支援常量模式。 桌面資料庫驅動程式支援 SQL-92 LIKE 模式匹配。  
  
 不支援在 LIKE 謂詞中使用轉義子句。  
  
 不應在包含數位或浮點數據類型數據的列上執行類似數據比較。 結果可能是不可預測的。 有關詳細資訊,請參閱 Microsoft*噴氣資料庫引擎程式師指南*。
