---
title: 字串長度及子字串的行為變更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18643dfc11d2b1b1d875a19c478f9ec8cbdd5be6
ms.sourcegitcommit: 5905c29b5531cef407b119ebf5a120316ad7b713
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66428843"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>字串長度及子字串行為的變更
  [String-length 函式&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length)並[substring 函數&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring)函式可能會傳回不同的結果與包含的 XML 資料庫搭配使用時surrogate 字元。  
  
## <a name="description"></a>描述  
 當資料庫設定為相容[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的行為[string-length 函式&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length)並[substring 函數&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring)函式變更處理 Unicode 補充字元時。 這些函數會將每個 Unicode 補充字元 (定義為具有大於 U+FFFF 的字碼指標) 計算成一個字元而非兩個，如同舊版的計算方式。  
  
 如需有關 surrogate 字元的詳細資訊，請參閱[Surrogate 和補充字元](https://go.microsoft.com/fwlink/?LinkId=178317)。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](https://docs.microsoft.com/sql/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
