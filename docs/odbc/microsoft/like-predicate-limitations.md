---
title: 述詞限制像 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 73e4ec1b4177b02869939628cb408df500958694
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="like-predicate-limitations"></a>像述詞限制
如果資料行中的長度超過 255 個字元，LIKE 比較會根據只有前 255 個字元。  
  
 在中使用類似的程序只支援常數的模式。 桌面資料庫驅動程式支援以 sql-92 像模式比對。  
  
 不支援使用 LIKE 述詞中逸出子句。  
  
 LIKE 比較不應該對該資料行包含數值或 float 資料類型的資料。 可能會無法預期的結果。 如需詳細資訊，請參閱*Microsoft Jet 資料庫引擎程式設計人員指南*。
