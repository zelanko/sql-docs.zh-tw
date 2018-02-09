---
title: "處理大型物件 (LOB) 參數，在 CLR 中的 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c9692632501eec31e517fb1bade2b3810c18c2b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>處理 CLR 中的大型物件 (LOB) 參數
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
使用**SqlBytes**和**SqlChars**傳遞大型物件 (LOB) 二進位類型 (**varbinary （max)**) 和 LOB 字元類型 (**nvarchar （max)**)參數，分別。 這些類型允許將 LOB 值從資料庫串流到 Common Language Runtime (CLR) 常式，而非將整個值複製到 Managed 空間。 **SqlBinary**和**SqlString**應透過僅適用於小型二進位和字元的字串值。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 中的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
