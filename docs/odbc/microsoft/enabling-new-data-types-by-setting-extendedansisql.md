---
description: 設定 ExtendedAnsiSQL 以啟用新資料類型
title: 藉由設定 ExtendedAnsiSQL 來啟用新的資料類型 |Microsoft Docs
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
ms.openlocfilehash: 609fdda7e56fe1c249df26da3f0117aab3634084
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412494"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>設定 ExtendedAnsiSQL 以啟用新資料類型
開啟 ExtendedAnsiSQL 旗標時，Jet 4.0 資料庫中有兩種新的資料類型： SQL_DECIMAL 和 SQL_NUMERIC。 預設的精確度和小數位數分別為18和0。 透過 ODBC 所存取的資料（輸入為 SQL_DECIMAL 或 SQL_NUMERIC）會對應至 Microsoft Jet Decimal 而非貨幣。  
  
 關閉 ExtendedAnsiSQL 旗標時，您無法建立具有 decimal 或 numeric 類型的資料表，且這些類型不會出現在 SQLGetTypeInfo ( # A1 中。 但是，如果資料表包含新的資料類型，就可以搭配正確的資料類型使用。
