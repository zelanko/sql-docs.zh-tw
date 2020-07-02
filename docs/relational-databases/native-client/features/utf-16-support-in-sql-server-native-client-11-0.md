---
title: UTF-16 支援
description: 從 SQL Server 2012 開始，瞭解 SQL Server Native Client 中固定長度緩衝區的 UTF-16 支援。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b538c19ebb1c0841ffb4da5ec403f5986d626e2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719628"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0 中的 UTF-16 支援
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  從開始 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ，如果您在系結資料行結果或輸出參數時提供固定長度的緩衝區，而且如果在終止字元之前寫入緩衝區的**wchar**字元是代理組的高代理程式碼點，而且下一個**wchar**字元是低代理程式碼點，則 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不會將高代理程式碼點加入緩衝區。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
