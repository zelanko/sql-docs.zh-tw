---
title: SQL Server Native Client 11.0 中的 utf-16 支援 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 66198f42676944967a2d655f14a27470922fd318
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135610"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0 中的 UTF-16 支援
  從開始[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，如果您在繫結資料行結果或輸出參數時提供固定長度的緩衝區，而且如果`wchar`結束的字元 surrogate 字組的高 surrogate 字碼指標之前，如果寫入緩衝區的字元下一步`wchar`字元是低 surrogate 字碼指標，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端不會將高 surrogate 字碼指標加入緩衝區。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  