---
description: SET ANSI 命令
title: 設定 ANSI 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a9f9c576199905c23994af4dc6b031114f4ad72
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466400"
---
# <a name="set-ansi-command"></a>SET ANSI 命令
決定如何使用 Visual FoxPro SQL 命令中的 = 運算子，在不同長度的字串之間進行比較。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 驅動程式 (預設值;Visual FoxPro 的預設值為 OFF。 ) 以所需的空格填補較短的字串，使其等於較長的字串長度。 然後，兩個字串會針對字元的整個長度進行比較。 請考慮下列比較：  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果為 False (。F. ) 如果設定的 ANSI 為 on，則在填補時，' Tom ' 會變成 ' Tom '，且字串 ' Tom ' 和 ' Tommy ' 不符合字元的字元。  
  
 = = 運算子會在 Visual FoxPro SQL 命令中使用這個方法來進行比較。  
  
 OFF  
 指定較短的字串不會填補空白。 這兩個字串會針對字元進行比較，直到到達較短字串的結尾為止。 請考慮下列比較：  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果為 True (。當 SET ANSI 為 off 時 ) ，因為比較在 ' Tom ' 之後停止。  
  
## <a name="remarks"></a>備註  
 SET ANSI 決定在進行 SQL 字串比較時，是否要將兩個字串中較短的空格填補空白。 SET ANSI 對 = = 運算子沒有任何作用;當您使用 = = 運算子時，較短的字串一律會以空格填補以進行比較。  
  
## <a name="string-order"></a>字串順序  
 在 SQL 命令中，比較中兩個字串的由左到右的順序，是從 = 或 = = 運算子的一端 irrelevantswitching 字串，而不會影響比較的結果。  
  
## <a name="see-also"></a>另請參閱  
 [SELECT-SQL 命令](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 命令](../../odbc/microsoft/set-exact-command.md)
