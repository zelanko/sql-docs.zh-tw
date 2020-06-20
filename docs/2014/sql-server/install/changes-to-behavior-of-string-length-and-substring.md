---
title: 字串長度和子字串行為的變更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1188823a877b4c5dc9cef13431492dfe3b303e23
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045000"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>字串長度及子字串行為的變更
  [字串長度函數 &#40;xquery&#41;](/sql/xquery/functions-on-string-values-string-length)和[Substring 函數 &#40;xquery&#41;](/sql/xquery/functions-on-string-values-substring)函數與包含代理字元的 XML 資料庫搭配使用時，可能會傳回不同的結果。  
  
## <a name="description"></a>描述  
 當資料庫設定為與相容時 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ，[字串長度函數 &#40;xquery&#41;](/sql/xquery/functions-on-string-values-string-length)和 substring 函式的行為，會在處理 Unicode 增補字元時[&#40;xquery&#41;](/sql/xquery/functions-on-string-values-substring)函數變更。 這些函數會將每個 Unicode 補充字元 (定義為具有大於 U+FFFF 的字碼指標) 計算成一個字元而非兩個，如同舊版的計算方式。  
  
 如需代理字元的詳細資訊，請參閱[代理和補充字元](https://go.microsoft.com/fwlink/?LinkId=178317)。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](https://docs.microsoft.com/sql/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
