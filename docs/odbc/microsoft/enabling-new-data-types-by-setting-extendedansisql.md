---
title: 啟用新的資料類型，藉由設定 ExtendedAnsiSQL |Microsoft 文件
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
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0b5c54555a8809c44a0fa3a65731ff4c6b591fc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>藉由設定 ExtendedAnsiSQL 啟用新的資料類型
兩個新的資料類型時，可以使用 Jet 4.0 資料庫中已開啟 ExtendedAnsiSQL 旗標： SQL_DECIMAL 和 SQL_NUMERIC。 預設有效位數和小數位數分別為 18 和 0。 透過 ODBC 型別為 SQL_DECIMAL 或 SQL_NUMERIC 存取的資料會對應到 Microsoft Jet 十進位而不是貨幣。  
  
 當 ExtendedAnsiSQL 旗標已關閉時，您無法使用十進位或數值類型，建立資料表，這些類型不會出現在 SQLGetTypeInfo()。 不過，如果資料表包含新的資料類型，它們可以用於具有正確的資料類型。
