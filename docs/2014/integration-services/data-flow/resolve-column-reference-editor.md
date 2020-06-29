---
title: 解析資料行參考編輯器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.resolvereferences.mapper.F1
- sql12.dts.designer.resolvereferences.preview.F1
ms.assetid: bb3ee33c-79c4-4c76-a82f-71581b4a60f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8b56e089feba35c3fe83e0a4e593309f8d1ac782
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431375"
---
# <a name="resolve-column-reference-editor"></a>解析資料行參考編輯器
  當輸入路徑中斷連接，或是如果路徑中有任何未對應的資料行，對應的資料路徑旁邊就會顯示錯誤圖示。 若要簡化資料行參考錯誤的解析，新的解析參考編輯器可讓您針對執行樹狀目錄中的所有路徑，將未對應的輸出資料行與未對應的輸入資料行連結。 解析參考編輯器也會反白顯示路徑，以指出正在解析哪些路徑。  
  
> [!NOTE]  
>  現在即使是元件的輸入路徑中斷連接，都可以編輯元件。  
  
 解析所有資料行參考之後，如果沒有其他資料路徑錯誤，資料路徑旁邊就不會顯示錯誤圖示。  
  
## <a name="options"></a>選項。  
 未對應的輸出資料行 (來源)：  
 上游路徑中目前未對應的資料行  
  
 對應的資料行 (來源)：  
 對應至下游路徑資料行的上游路徑資料行  
  
 對應的資料行 (目的地)：  
 對應至下游路徑資料行的上游路徑資料行  
  
 未對應的輸入資料行 (目的地)：  
 下游路徑中目前未對應的資料行  
  
 刪除未對應的輸入資料行  
 核取「刪除未對應的輸入資料行」，以忽略資料路徑目的地的未對應資料行。 [預覽變更] 按鈕會顯示當您按下 [確定] 按鈕時，將會出現的變更清單。  
  
  
