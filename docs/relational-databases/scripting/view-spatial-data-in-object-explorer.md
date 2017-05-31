---
title: "檢視物件總管中的空間資料 | Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 59cca562-e3f5-4257-b868-adcbcc0142cc
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c5757bcb84f441e81f3da7b91e6acf449696cc30
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="view-spatial-data-in-object-explorer"></a>檢視物件總管中的空間資料
  除了以方格格式顯示在 [結果] 視窗中的資料以外，查詢編輯器中的 [空間結果] 視窗還會提供檢視空間資料結果的視覺化對應工具。 若要在 [空間結果] 視窗中顯示空間資料，您的查詢結果至少必須包含一個具有幾何或地理位置資料的空間資料行。  
  
### <a name="to-view-spatial-data-in-the-spatial-results-window"></a>在空間結果視窗中檢視空間資料  
  
1.  在查詢編輯器中，按一下 [空間結果] 索引標籤。  
  
    > [!NOTE]  
    >  如果您的查詢結果沒有包含空間資料，或者您指定要將結果傳回成文字，就無法使用這個視窗。  
  
2.  在 [選取空間資料行] 清單中，選取您想要檢視的資料行。 如果您的資料表只有一個空間資料行，這個資料行就是清單中的預設選項。  
  
3.  在 [選取標籤資料行] 清單中，選取您想要當作資料標籤使用的非空間資料行。  
  
4.  在 [選取投射] 清單中，選取您想要針對地理位置資料使用的投射。 預設投射為 Equirectangular。其他可用的投射包括 Mercator、Robinson 或 Bonne。  
  
    > [!NOTE]  
    >  如果您的空間資料行包含幾何資料，就無法使用 [選取投射]。  
  
5.  調整 [顯示比例] 滑動軸，以便增加對應元素的視覺大小。 若為多邊形形狀，只有當此形狀夠大，足以容納標籤文字時，才會顯示標籤。  
  
## <a name="see-also"></a>另請參閱  
 [空間結果視窗](../../relational-databases/scripting/spatial-results-window.md)   
 [Database Engine 查詢編輯器 &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)   
 [查詢與文字編輯器 &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
