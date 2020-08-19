---
description: LIKE 述詞限制
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
ms.openlocfilehash: 63410b78b6d0b7ab59dd74b9f69fe57fe498c6ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483521"
---
# <a name="like-predicate-limitations"></a>LIKE 述詞限制
如果資料行中的資料長度超過255個字元，則 LIKE 比較只會以前255個字元為基礎。  
  
 只有常數模式才支援程式中所使用的。 桌面資料庫驅動程式支援類似 SQL-92，例如模式比對。  
  
 不支援在 LIKE 述詞中使用 escape 子句。  
  
 在包含數值或 float 資料類型之資料的資料行上，不應該執行 LIKE 比較。 結果可能無法預期。 如需詳細資訊，請參閱《 *Microsoft Jet 資料庫引擎程式設計人員指南》*。
