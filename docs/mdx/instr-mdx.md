---
description: Instr (MDX)
title: " (MDX) 的 Instr |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 877fc4658081108e810e404dfc8d4a368c6964ba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387354"
---
# <a name="instr-mdx"></a>Instr (MDX)


  傳回一個字串在另一個字串中第一次出現的位置。  
  
## <a name="syntax"></a>語法  
  
```  
InStr([start, ]searched_string, search_string[, compare])  
```  
  
## <a name="arguments"></a>引數  
 *開始*  
 (選擇性) 數值運算式，設定每次搜尋的開始位置。 如果省略此值，則會在第一個字元位置開始搜尋。 如果 start 是 null，則函數傳回值未定義。  
  
 *searched_string*  
 要搜尋的字串運算式。  
  
 *search_string*  
 搜尋目標的字串運算式。  
  
 *比較*  
 (選擇性) 整數值。 一律會忽略這個引數。 它是為了與其他語言中的其他 **Instr** 函數相容而定義的。  
  
## <a name="return-value"></a>傳回值  
 以*string1*開始位置為*string2*的整數值。  
  
 此外， **InStr** 函數會根據條件傳回下表所列的值：  
  
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
>  **Instr** 一律會執行不區分大小寫的比較。  
  
## <a name="example"></a>範例  
 下列範例顯示 **Instr** 函數的用法，並顯示不同的結果案例。  
  
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
  
|量值中的欄位|結果|  
|-|-|  
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
  
  
