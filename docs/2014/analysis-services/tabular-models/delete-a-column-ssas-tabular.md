---
title: 刪除資料行 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 703db83b-e554-450e-813e-23ad08c1cdad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f0a95e8580aa30ce34ada1c77e198eb40d767304
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067265"
---
# <a name="delete-a-column-ssas-tabular"></a>刪除資料行 (SSAS 表格式)
  本主題描述的是如何從表格式模型資料表中刪除資料行。  
  
## <a name="delete-a-model-table-column"></a>刪除模型資料表資料行  
  
> [!NOTE]  
>  從模型資料表中刪除資料行時，並不會從資料分割查詢定義中刪除該資料行。 如果您要刪除的資料行屬於資料分割的一部分，就必須從資料分割查詢定義中手動刪除該資料行。 如果沒有從資料分割查詢定義中刪除資料行，將會導致系統在處理作業期間查詢該資料行並且傳回資料，但是不會擴展至模型資料表。 如需詳細資訊，請參閱 [資料分割 &#40;SSAS 表格式&#41;](partitions-ssas-tabular.md)。  
  
#### <a name="to-delete-a-model-table-column"></a>若要刪除模型資料表資料行  
  
-   在模型設計師中，於包含您想要刪除之資料行的資料表內，以滑鼠右鍵按一下資料行，然後按一下 [刪除]  。  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>若要使用資料表屬性對話方塊來刪除模型資料表資料行  
  
1.  在模型設計師中，按一下包含您想要刪除之資料行的資料表、按一下 [資料表]  功能表，然後按一下 [資料表屬性]  。  
  
2.  在 [資料行名稱來自]  中，選取 [模型]  (使用模型資料表資料行名稱，如果與來源不同的話  )。  
  
3.  在 [編輯資料表屬性]  對話方塊的 [資料表預覽] 視窗中，取消核取您想要刪除的資料行，然後按一下 [確定]  。  
  
## <a name="see-also"></a>另請參閱  
 [將資料行加入至資料表 &#40;SSAS 表格式&#41;](add-columns-to-a-table-ssas-tabular.md)   
 [資料分割 &#40;SSAS 表格式&#41;](partitions-ssas-tabular.md)  
  
  
