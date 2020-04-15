---
title: 通過設定擴展安西SQL 啟用新數據類型 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b703c5c14c4743e13feee139d16e5dfeb3c24c63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303409"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>設定 ExtendedAnsiSQL 以啟用新資料類型
打開擴展安西SQL 標誌時,Jet 4.0 資料庫中有兩種新的數據類型:SQL_DECIMAL和SQL_NUMERIC。 預設精度和比例分別為 18 和 0。 通過 ODBC 訪問的資料鍵入為SQL_DECIMAL或SQL_NUMERIC將映射到 Microsoft Jet 十進位,而不是貨幣。  
  
 關閉擴展 AnsiSQL 標誌後,無法建立具有小數或數位類型的表,並且這些類型將不會顯示在 SQLGetTypeInfo() 中。 但是,如果表包含新的數據類型,則可以將它們與正確的數據類型一起使用。
