---
title: 工作13：新增 OLE DB 目的地，以將資料寫入 MDS 臨時表 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7c5fc9d863c23c1cae08c04fef7810aeda446762
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65476989"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>工作 13：加入 OLE DB 目的地，以便將資料寫入 MDS 暫存資料表
  現在您已將**ImportType**和**BatchTag**值新增至所有記錄，您已準備好將它們傳送至 MDS 進行預備。 在這項工作中，您會使用 OLE DB 目的地，將資料寫入**stg.< 中。 supplier_Leaf**臨時表。  
  
1.  將 [ **SSIS 工具箱**] 中 [**其他目的地**] 區段的 [ **OLE DB 目的地**] 拖曳至 [**資料流程**] 索引標籤，然後將它放置在 [**加入 MDS 所需的欄位**  
  
2.  以滑鼠右鍵**按一下 [資料流程**] 索引標籤中**OLE DB 目的地**]，然後按一下 [**重新命名**]。 輸入**將供應商資料寫入 MDS 臨時表**，然後按**enter**。  
  
3.  連接**Mds 所需的新增資料行**，以使用藍色連接器將**供應商資料寫入 mds 臨時表**。  
  
4.  按兩下 **[資料流程**] 索引標籤中的 [**將供應商資料寫入 MDS 臨時表**]。  
  
5.  在 [ **OLE DB 目的地編輯器**] 對話方塊中，確認 **[（本機）]。MDS** （或**localhost。MDS**）選取 [ **OLE DB 連接管理員**] 欄位。  
  
6.  選取 [ **stg.<]。Supplier_Leaf**資料表**或視圖名稱**清單中的資料表。  
  
     ![OLEDB 目的地編輯器](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "OLEDB 目的地編輯器")  
  
7.  按一下左側功能表**上的 [** 對應]，切換至 [**對應**] 頁面。  
  
8.  對應**輸入**和**目的地**資料行，如下表所示。  
  
     ![OLEDB 目的地編輯器 - 對應](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "OLEDB 目的地編輯器 - 對應")  
  
9. 請確認您使用的是輸入資料行的 **_Output**資料行，而不是 **_Status**或 **_Source**資料行。 **_Output**資料行包含 DQS 清理的輸出值。  
  
10. 按一下 **[確定]** 以關閉 [ **OLE DB 目的地編輯器**] 對話方塊。  
  
11. 資料流程應該類似下圖。  
  
     ![完成的資料流程](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "完成的資料流程")  
  
## <a name="next-step"></a>後續步驟  
 [工作 14：將執行 SQL 工作加入到控制流程，為 MDS 執行預存程序](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
