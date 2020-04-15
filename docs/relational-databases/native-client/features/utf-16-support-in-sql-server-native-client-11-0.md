---
title: SQL 伺服器本機用戶端 11.0 中的 UTF-16 支援 |微軟文件
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
ms.openlocfilehash: 56a368c8b01e1afec2fab5de5eb3c575c6ebdf14
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303159"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0 中的 UTF-16 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]中開始,如果在綁定列結果或輸出參數時提供固定長度緩衝區,並且在終止字元之前寫入緩衝區的**wchar**字元是代理項對的高代理項代碼點,並且下一個**wchar**字元是[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]低代理程式碼點, 本機用戶端將不會向緩衝區添加高代理代碼點。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
