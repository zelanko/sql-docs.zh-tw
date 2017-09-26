---
title: "解析資料行參考編輯器 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.resolvereferences.preview.F1
- sql13.dts.designer.resolvereferences.mapper.F1
ms.assetid: bb3ee33c-79c4-4c76-a82f-71581b4a60f1
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2ff8a97d45d75c3e93d4aa3111b653c9612b889
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="resolve-column-reference-editor"></a>解析資料行參考編輯器
  當輸入路徑中斷連接，或是如果路徑中有任何未對應的資料行，對應的資料路徑旁邊就會顯示錯誤圖示。 若要簡化資料行參考錯誤的解析，解析參考編輯器可讓您未對應的輸出資料行與未對應的輸入資料行的執行樹狀目錄中的所有路徑的連結。 解析參考編輯器也會反白顯示路徑，以指出正在解析哪些路徑。  
  
> [!NOTE]  
>  您可編輯的元件，即使其輸入的路徑中斷連接  
  
 解析所有資料行參考之後，如果沒有其他資料路徑錯誤，資料路徑旁邊就不會顯示錯誤圖示。  
  
## <a name="options"></a>選項。  
 **未對應的輸出資料行 （來源）**    
 上游路徑中目前未對應的資料行  
  
**對應的資料行 （來源）**    
 對應至下游路徑資料行的上游路徑資料行  
  
**對應的資料行 （目的地）**    
 對應至下游路徑資料行的上游路徑資料行  
  
**未對應的輸入資料行 （目的地）**    
 下游路徑中目前未對應的資料行  
  
**刪除未對應的輸入資料行**  
 核取「刪除未對應的輸入資料行」，以忽略資料路徑目的地的未對應資料行。 [預覽變更] 按鈕會顯示當您按下 [確定] 按鈕時，將會出現的變更清單。  
  
  
