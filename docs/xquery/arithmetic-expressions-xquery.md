---
title: 算術運算式（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
author: rothja
ms.author: jroth
ms.openlocfilehash: ccbeda01726a3473f8e955676c3ebd62a93fd630
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67985733"
---
# <a name="arithmetic-expressions-xquery"></a>算術運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  除了**idiv**以外，所有算術運算子都受到支援。 以下範例說明算術運算子的基本用法：  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 因為不支援**idiv** ，所以解決方案是使用**xs： integer （）** 的函式：  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 算術運算子的結果類型式是以輸入值的類型為基礎。 如果運算元的類型不同，會在需要時根據類型階層，將其中之一或兩者都轉換成一般的 Primitive 基本類型。 如需類型階層的詳細資訊，請參閱[XQuery 中的類型轉換規則](../xquery/type-casting-rules-in-xquery.md)。  
  
 如果兩個運算是不同的數值基本類型，就會發生數值類型升級。 例如，將**xs： decimal**加入**xs： double**會先將十進位值變更為 double。 接下來，執行結果為 double 值的加法。  
  
 不具類型的不可部份完成值會轉換成另一個運算元的數值基底類型，如果另一個運算元也不具類型，則為**xs： double** 。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   算術運算子的引數必須是數數值型別或**untypedAtomic**。  
  
-   **Xs： integer**值的作業會產生**xs： decimal**類型的值，而不是**xs： integer**。  
  
  
