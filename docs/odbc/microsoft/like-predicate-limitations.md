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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8cd3cebfcf20df2f8a3a786ea66fd28dd76307c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68119713"
---
# <a name="like-predicate-limitations"></a>LIKE 述詞限制
如果資料行中的資料長度超過255個字元，則 LIKE 比較只會以前255個字元為基礎。  
  
 只有常數模式才支援在程式中使用的 LIKE。 桌面資料庫驅動程式支援類似模式比對的 SQL-92。  
  
 在 LIKE 述詞中不支援使用 escape 子句。  
  
 您不應該在包含數值或 float 資料類型之資料的資料行上執行 LIKE 比較。 結果可能無法預測。 如需詳細資訊，請參閱《 *Microsoft Jet 資料庫引擎程式設計人員指南》*。
