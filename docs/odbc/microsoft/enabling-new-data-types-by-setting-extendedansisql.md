---
title: 設定 extendedansisql 來啟用新的資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80a86ef188796883e76c6d5f6149a3e40afd341b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128000"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>設定 ExtendedAnsiSQL 以啟用新資料類型
開啟 ExtendedAnsiSQL 旗標時，兩個新的資料類型是 Jet 4.0 資料庫中可用：SQL_DECIMAL 和 SQL_NUMERIC。 預設有效位數和小數位數分別為 18 和 0。 透過 ODBC 類型 SQL_DECIMAL 或 SQL_NUMERIC 為存取的資料會對應到 Microsoft Jet 十進位而不是貨幣。  
  
 ExtendedAnsiSQL 旗標為關閉時，您無法使用十進位或數值類型，來建立資料表，這些類型不會出現在 SQLGetTypeInfo()。 不過，如果資料表包含新的資料類型，它們可以搭配正確的資料類型。
