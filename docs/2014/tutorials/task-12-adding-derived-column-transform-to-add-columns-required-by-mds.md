---
title: 工作 12： 加入衍生的資料行轉換，以加入 MDS 所需的資料行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6d1bb94b040aee5ba1db6870edc71e3153a3c7a4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165709"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>工作 12：加入衍生的資料行轉換，以加入 MDS 需要的資料行
  在這項工作中，您會將衍生的資料行轉換加入至資料流程。 新增兩個衍生的資料行**ImportType**並**BatchTag**至記錄傳遞給這項轉換。 您應該先加入這兩個資料行，然後再將資料上傳至 MDS 中的暫存資料表。 這兩個是 MDS 中暫存資料表的必要資料行。 請參閱[分葉成員暫存資料表](http://msdn.microsoft.com/library/ee633854.aspx)如需詳細資訊。  
  
1.  拖放**衍生的資料行轉換**從**常見**一節中**SSIS 工具箱**至**資料流程** 索引標籤。  
  
2.  以滑鼠右鍵按一下**衍生的資料行**轉換**資料流程**索引標籤，然後按一下**重新命名**。 型別**加入 MDS 所需的資料行**然後按**ENTER**。  
  
3.  連接**篩選重複項**要**加入 MDS 所需的資料行**使用藍色連接器。 您應該會看到**輸入輸出選擇** 對話方塊。  
  
4.  中**輸入輸出選擇**對話方塊中，選取**唯一記錄**，然後按一下**確定**。  
  
     ![輸入輸出選擇 對話方塊](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "輸入輸出選擇 對話方塊")  
  
5.  按一下 [ **SSIS** ] 功能表列上按一下**變數**。  
  
6.  在 [**變數**] 視窗中，按一下**加入變數**工具列上的按鈕。  
  
     ![SSIS 變數視窗](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "SSIS 變數視窗")  
  
7.  型別**ImportType** for**名稱**並**2**如**值**。 您指定的值為 2，因為您要在 MDS 的實體中加入新的成員。 如需有關此參數的詳細資訊，請參閱 <<c0> [ 分葉成員暫存資料表](http://msdn.microsoft.com/library/ee633854.aspx)。  
  
8.  按一下 **加入變數**工具列按鈕一次。  
  
9. 型別**BatchTag**如**名稱**，選取**字串**如**資料類型**，和**EIMBatch**的**值**。 **BatchTag**是只要您將提交給 MDS 之批次的唯一名稱。  
  
10. 在 **資料流程**索引標籤上，按兩下**加入 MDS 所需的資料行**。  
  
11. 在**衍生的資料行轉換編輯器**對話方塊中，於**清單方塊的下方窗格中**，型別**ImportType**如**衍生資料行名稱**.  
  
12. 依序展開**變數和參數**在左上方窗格中，拖曳**user:: importtype**來**運算式**資料行。  
  
     ![衍生資料行轉換編輯器](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "衍生資料行轉換編輯器")  
  
13. 型別**BatchTag**中的下一個資料列**衍生的資料行名稱**。  
  
14. 拖放**user:: batchtag**從**變數和參數**來**運算式**資料行。  
  
15. 按一下 [ **[確定]** 以關閉**衍生的資料行轉換**] 對話方塊。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 13：新增 OLE DB 目的地，以便將資料寫入 MDS 暫存資料表](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
