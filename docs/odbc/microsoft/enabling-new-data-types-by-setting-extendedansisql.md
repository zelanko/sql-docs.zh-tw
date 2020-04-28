---
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
ms.openlocfilehash: b703c5c14c4743e13feee139d16e5dfeb3c24c63
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303409"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>設定 ExtendedAnsiSQL 以啟用新資料類型
當 ExtendedAnsiSQL 旗標開啟時，Jet 4.0 資料庫中有兩種新的資料類型： SQL_DECIMAL 和 SQL_NUMERIC。 預設的精確度和小數位數分別為18和0。 透過 ODBC 存取的資料（類型為 SQL_DECIMAL 或 SQL_NUMERIC）會對應至 Microsoft Jet Decimal，而不是貨幣。  
  
 當 ExtendedAnsiSQL 旗標已關閉時，您無法建立具有 decimal 或 numeric 類型的資料表，而且這些類型不會出現在 SQLGetTypeInfo （）中。 不過，如果資料表包含新的資料類型，它們可以與正確的資料類型搭配使用。
