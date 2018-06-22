---
title: SQL Server Native Client 11.0 中的 utf-16 支援 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2796da7d9b3e2875cfb6c2e3033e2615ad021ecc
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698409"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0 中的 UTF-16 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  從開始[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，如果您在繫結資料行結果或輸出參數時提供固定長度的緩衝區，而且如果**wchar**結束的字元為高 surrogate 字碼指標之前寫入緩衝區的字元surrogate 字組，而且如果下一個**wchar**字元是低 surrogate 字碼指標，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端不會將高 surrogate 字碼指標加入緩衝區。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
