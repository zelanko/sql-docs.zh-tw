---
title: 處理大型物件 (LOB) 參數，在 CLR 中的 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 58b2e188a69799dd0b8d36958a7059d5cfcc09f9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136873"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>處理 CLR 中的大型物件 (LOB) 參數
  使用 `SqlBytes` 和 `SqlChars` 分別傳遞大型物件 (LOB) 二進位類型 (`varbinary(max)`) 和 LOB 字元類型 (`nvarchar(max)`) 參數。 這些類型允許將 LOB 值從資料庫串流到 Common Language Runtime (CLR) 常式，而非將整個值複製到 Managed 空間。 `SqlBinary` 和 `SqlString` 應該僅用於小型二進位和字元字串值。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](sql-server-data-types-in-the-net-framework.md)  
  
  