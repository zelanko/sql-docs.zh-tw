---
title: 算術運算式 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3d970209b71a842aa1c78b2f7dd0db980e0ce73e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642646"
---
# <a name="arithmetic-expressions-xquery"></a>算術運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  支援所有算術運算子，除了**idiv&lt**。 以下範例說明算術運算子的基本用法：  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 因為**idiv&lt**是不受支援，解決方案是使用**xs:integer()** 建構函式：  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 算術運算子的結果類型式是以輸入值的類型為基礎。 如果運算元的類型不同，會在需要時根據類型階層，將其中之一或兩者都轉換成一般的 Primitive 基本類型。 如需類型階層的資訊，請參閱[XQuery 中的類型轉換規則](../xquery/type-casting-rules-in-xquery.md)。  
  
 如果兩個運算是不同的數值基本類型，就會發生數值類型升級。 例如，新增**xs: decimal**要**xs: double**會先將十進位值變更為雙精度浮點數。 接下來，執行結果為 double 值的加法。  
  
 不具類型的不可部份完成值會轉換到另一個運算元的數字的基底型別或**xs: double**如果其他運算元也是不具型別。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   針對算術運算子的引數必須是數值類型或**untypedAtomic**。  
  
-   上的作業**xs: integer**值類型的值會產生**xs: decimal**而非**xs: integer**。  
  
  
