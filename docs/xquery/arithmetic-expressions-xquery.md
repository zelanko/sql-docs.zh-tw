---
title: "算術運算式 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ba5c642195f1049f7df59a0fa14ef666eec4bfe
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="arithmetic-expressions-xquery"></a>算術運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  支援所有算術運算子，除了**i**。 以下範例說明算術運算子的基本用法：  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 因為**i**是不受支援，解決方案是使用**xs:integer()**建構函式：  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 算術運算子的結果類型式是以輸入值的類型為基礎。 如果運算元的類型不同，會在需要時根據類型階層，將其中之一或兩者都轉換成一般的 Primitive 基本類型。 如需類型階層的資訊，請參閱[XQuery 中的類型轉換規則](../xquery/type-casting-rules-in-xquery.md)。  
  
 如果兩個運算是不同的數值基本類型，就會發生數值類型升級。 例如，加入**xs: decimal**至**xs: double**會先變更成雙精度浮點數的十進位值。 接下來，執行結果為 double 值的加法。  
  
 不具類型的不可部份完成值會轉換為另一個運算元數字的基底型別，或**xs: double**如果其他運算元也是不具型別。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   針對算術運算子的引數必須是數值類型或**untypedAtomic**。  
  
-   上的作業**xs: integer**值類型的值會產生**xs: decimal**而不是**xs: integer**。  
  
  

