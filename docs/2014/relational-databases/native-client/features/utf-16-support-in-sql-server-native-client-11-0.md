---
title: SQL Server Native Client 11.0 中的 UTF-16 支援 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b28d869a6e33969550751158e321ec24062bf6ac
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707151"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0 中的 UTF-16 支援
  從開始 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ，如果您在系結資料行結果或輸出參數時提供固定長度的緩衝區，而且如果在 `wchar` 終止字元之前寫入緩衝區的字元是代理組的高代理程式碼點，而且下一個 `wchar` 字元是低代理程式碼點，則 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不會將高代理程式碼點加入緩衝區。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
