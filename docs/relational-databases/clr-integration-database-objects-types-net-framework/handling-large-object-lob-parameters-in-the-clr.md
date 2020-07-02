---
title: 處理 CLR 中的大型物件（LOB）參數 |Microsoft Docs
description: 本文說明如何在 SQL Server CLR 整合中處理參數的大型物件（LOB）值。 針對 LOB 類型，請使用 SqlBytes 和 SqlChars。
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b10ac8c1ac9ccba804b892617df0b8d6c0d2f14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637484"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>處理 CLR 中的大型物件 (LOB) 參數
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  使用**SqlBytes**和**SqlChars** ，分別傳遞大型物件（LOB）二進位類型（**Varbinary （max）**）和 LOB 字元類型（**Nvarchar （max）**）參數。 這些類型允許將 LOB 值從資料庫串流到 Common Language Runtime (CLR) 常式，而非將整個值複製到 Managed 空間。 **SqlBinary**和**SqlString**只能用於小型二進位和字元字串值。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
