---
title: Instr (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 5638c358-47da-40ad-b988-1a5214c05492
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: d269dbaed6c3adc208d4b81b3cbf3af30c3de26d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="instr-mdx"></a>Instr (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回一個字串在另一個字串中第一次出現的位置。  
  
## <a name="syntax"></a>語法  
  
```  
InStr([start, ]searched_string, search_string[, compare])  
```  
  
## <a name="arguments"></a>引數  
 *start*  
 (選擇性) 數值運算式，設定每次搜尋的開始位置。 如果省略此值，則會在第一個字元位置開始搜尋。 如果 start 是 null，則函數傳回值未定義。  
  
 *searched_string*  
 要搜尋的字串運算式。  
  
 *search_string*  
 搜尋目標的字串運算式。  
  
 *比較*  
 (選擇性) 整數值。 一律會忽略這個引數。 定義與其他相容性**Instr**其他語言中的函式。  
  
## <a name="return-value"></a>傳回值  
 整數值的開始位置與*String2*中*String1*。  
  
 此外， **InStr**函式會傳回的值列於下表根據條件：  
  
|條件|傳回值|  
|---------------|------------------|  
|String1 為零長度|零 (0)|  
|String1 為 Null|未定義|  
|String2 為零長度|start|  
|String2 為 Null|未定義|  
|找不到 String2|零 (0)|  
|start 大於 Len(String2)|零 (0)|  
  
## <a name="remarks"></a>備註  
  
> [!WARNING]  
>  **Instr**一律會執行不區分大小寫的比較。  
  
## <a name="example"></a>範例  
 下列範例示範使用**Instr**函式並顯示不同的結果案例。  
  
```  
with   
    member [Date].[Date].[Results] as "Results"  
    member measures.[lowercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[uppercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "O")  
    member measures.[searched string is empty]            as InStr( "", "o")  
    member measures.[searched string is null]             as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[search string is empty]              as InStr( "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is empty start 10]     as InStr(10, "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is null]               as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[found from start 10]                 as InStr( 10, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NOT found from start 17]             as InStr( 17, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NULL start]                          as iif(IsError(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Error", iif(IsNull(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Null","Is undefined"))  
    member measures.[start greater than searched length]  as InStr( 170, "abcdefghijklmnñopqrstuvwxyz", "o")  
  
select  [Results] on columns,  
       { measures.[lowercase found in lowercase string]  
       , measures.[uppercase found in lowercase string]  
       , measures.[searched string is empty]  
       , measures.[searched string is null]  
       , measures.[search string is empty]  
       , measures.[search string is empty start 10]  
       , measures.[search string is null]  
       , measures.[found from start 10]  
       , measures.[NOT found from start 17]  
       , measures.[NULL start]   
       , measures.[start greater than searched length]  
       } on rows  
  
from [Adventure Works]  
```  
  
 下表會顯示取得的結果。  
  
|||  
|-|-|  
||結果|  
|小寫字串中找到小寫|16|  
|小寫字串中找到大寫|16|  
|搜尋的字串是空的|0|  
|搜尋的字串是 Null|未定義|  
|搜尋的字串是空的|1|  
|搜尋字串從 10 開始處為空的|10|  
|搜尋字串是 Null|未定義|  
|從 10 開始處找到|16|  
|從 17 開始處找不到|0|  
|NULL 開始|未定義|  
|開始處大於已搜尋的長度|0|  
  
  
