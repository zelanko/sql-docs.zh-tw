---
title: 工作 13： 加入 OLE DB 目的地，將資料寫入 MDS 暫存資料表 |Microsoft 文件
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
ms.topic: article
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 75e77579857852e607b783534d149367a946318f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031535"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>工作 13：加入 OLE DB 目的地，以便將資料寫入 MDS 暫存資料表
  既然您已加入**ImportType**和**BatchTag**所有記錄的值，您準備好將它們傳送到 MDS 供暫存。 在這個工作中，您可以使用 OLE DB 目的地寫入資料**stg.supplier_Leaf**暫存資料表。  
  
1.  拖曳**OLE DB 目的地**從**其他目的地**一節中**SSIS 工具箱**至**資料流程**索引標籤上，並將它放下方**加入 MDS 所需的資料行**。  
  
2.  以滑鼠右鍵按一下**OLE DB 目的地**中**資料流程**索引標籤，然後按一下**重新命名**。 型別**供應商資料寫入 MDS 暫存資料表**按**ENTER**。  
  
3.  連接**加入 MDS 所需的資料行**至**供應商資料寫入 MDS 暫存資料表**使用藍色連接器。  
  
4.  按兩下**供應商資料寫入 MDS 暫存資料表**中**資料流程** 索引標籤。  
  
5.  在**OLE DB 目的地編輯器**對話方塊方塊中，請確定 **（本機）。MDS** (或**localhost。MDS**) 選取**OLE DB 連接管理員**欄位。  
  
6.  選取**stg.<Supplier_Leaf**從清單中的資料表**的資料表或檢視表名稱**。  
  
     ![OLEDB 目的地編輯器](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "OLEDB 目的地編輯器")  
  
7.  切換至**對應**頁面，即可**對應**左邊功能表上。  
  
8.  地圖**輸入**和**目的地**下表所示的資料行。  
  
     ![OLEDB 目的地編輯器-對應](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "OLEDB 目的地編輯器-對應")  
  
9. 確認您使用 **_Output**之輸入資料行，不 **_Status**或 **_Source**資料行。 **_Output**資料行包含 DQS 清理的輸出值。  
  
10. 按一下**確定**關閉**OLE DB 目的地編輯器** 對話方塊。  
  
11. 資料流程應該類似下圖。  
  
     ![完成資料流程](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "完成資料流程")  
  
## <a name="next-step"></a>下一個步驟  
 [工作 14： 將執行 SQL 工作，為 MDS 執行預存程序的控制流程](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  