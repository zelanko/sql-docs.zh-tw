---
title: LIKE 述詞限制 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298958"
---
# <a name="like-predicate-limitations"></a>LIKE 述詞限制
如果資料行中的資料長度超過255個字元，則 LIKE 比較只會以前255個字元為基礎。  
  
 只有常數模式才支援在程式中使用的 LIKE。 桌面資料庫驅動程式支援類似模式比對的 SQL-92。  
  
 在 LIKE 述詞中不支援使用 escape 子句。  
  
 您不應該在包含數值或 float 資料類型之資料的資料行上執行 LIKE 比較。 結果可能無法預測。 如需詳細資訊，請參閱《 *Microsoft Jet 資料庫引擎程式設計人員指南》*。
