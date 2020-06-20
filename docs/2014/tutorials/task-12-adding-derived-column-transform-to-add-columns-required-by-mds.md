---
title: 工作12：加入衍生的資料行轉換，以加入 MDS 所需的資料行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 8eac057177032892ac99f557aa9d18ce497b7b2f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054284"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>工作 12：新增衍生的資料行轉換來新增 MDS 需要的資料行
  在這項工作中，您會將衍生的資料行轉換加入至資料流程。 您可以將兩個衍生的資料行**ImportType**和**BatchTag**加入至傳遞給此轉換的記錄。 您應該先加入這兩個資料行，然後再將資料上傳至 MDS 中的暫存資料表。 這兩個是 MDS 中暫存資料表的必要資料行。 如需詳細資訊，請參閱分[葉成員臨時表](../master-data-services/leaf-member-staging-table-master-data-services.md)。  
  
1.  從 [ **SSIS 工具箱**] 的 [**一般**] 區段，將 [衍生的**資料****行轉換**] 拖放至 [資料流程] 索引標籤  
  
2.  以滑鼠右鍵按一下 [資料流程] 索引標籤中的 [衍生**資料****行**轉換]，然後按一下 [**重新命名**] 輸入 [**加入 MDS 所需的資料行**]，然後按**enter**。  
  
3.  連接**篩選重複專案**，以使用藍色連接器**加入 MDS 所需的資料行**。 您應該會看到 [**輸入輸出選擇**] 對話方塊。  
  
4.  在 [**輸入輸出選擇**] 對話方塊中，選取 [**唯一記錄**]，然後按一下 **[確定]**。  
  
     ![[輸入輸出選擇] 對話方塊](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "[輸入輸出選擇] 對話方塊")  
  
5.  按一下功能表列上的 [ **SSIS** ]，然後按一下 [**變數**]。  
  
6.  在 [**變數**] 視窗中，按一下工具列上的 [**加入變數**] 按鈕。  
  
     ![SSIS 變數視窗](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "SSIS 變數視窗")  
  
7.  在 [**名稱**] 中輸入**ImportType** ，並在 [**值**] 中輸入**2** 。 您指定的值為 2，因為您要在 MDS 的實體中加入新的成員。 如需這個參數的詳細資訊，請參閱分[葉成員臨時表](../master-data-services/leaf-member-staging-table-master-data-services.md)。  
  
8.  再次按一下 [**新增變數**] 工具列按鈕。  
  
9. 在 [**名稱**] 中輸入**BatchTag** ，針對**資料類型**選取 [**字串**]，並針對 [**值**] **EIMBatch** 。 **BatchTag**只是您將提交至 MDS 的批次唯一名稱。  
  
10. 在 [資料流程] 索引標籤中，按兩下 [**加入 MDS 所需的****資料**行]。  
  
11. 在 [**衍生的資料行轉換編輯器**] 對話方塊中，于**底部窗格的清單方塊**中，針對 [**衍生的資料行名稱**] 輸入**ImportType** 。  
  
12. 展開左上方窗格中的 [**變數和參數**]，將**User：： ImportType**拖放到 [**運算式**] 資料行。  
  
     ![衍生的資料行轉換編輯器](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "衍生的資料行轉換編輯器")  
  
13. 在 [衍生的資料行名稱] 的下一個資料**列**中，輸入**BatchTag** 。  
  
14. 將**User：： BatchTag**從**變數和參數**拖放至**Expression**資料行。  
  
15. 按一下 **[確定]** 以關閉 [衍生的資料**行轉換**] 對話方塊。  
  
## <a name="next-step"></a>後續步驟  
 [工作 13：新增 OLE DB 目的地來將資料寫入 MDS 暫存資料表](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
