---
title: SQL Server Native Client 11.0 中的 UTF-16 支援 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 415cb2fe8a3295770cfc8bd2d5c6e56750adb6d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63205120"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0 中的 UTF-16 支援
  從開始[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，如果您在系結資料行結果或輸出參數時提供固定長度的緩衝區，而且`wchar`如果在終止字元之前寫入緩衝區的字元是代理組的高代理程式碼點，而且下一個`wchar`字元是低代理程式碼點， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]則 Native Client 不會將高代理程式碼點加入緩衝區。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
