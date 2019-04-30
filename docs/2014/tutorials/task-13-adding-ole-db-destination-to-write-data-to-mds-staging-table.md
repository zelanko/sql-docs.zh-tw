---
title: 工作 13：加入將資料寫入 MDS 暫存資料表的 OLE DB 目的地 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 34f68c4604d70dc83579f8c9284802b82cc6291d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222612"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>工作 13：新增 OLE DB 目的地來將資料寫入 MDS 暫存資料表
  既然您已新增**ImportType**並**BatchTag**所有記錄的值，您已準備好將它們傳送至 MDS 供暫存。 在這個工作中，您可以使用 OLE DB 目的地將資料寫入至**stg.supplier_Leaf**暫存資料表。  
  
1.  拖曳**OLE DB 目的地**從**其他目的地**一節中**SSIS 工具箱**至**資料流程**索引標籤並將它放在**加入 MDS 所需的資料行**。  
  
2.  以滑鼠右鍵按一下**OLE DB 目的地**中**資料流程**索引標籤，然後按一下**重新命名**。 型別**供應商資料寫入 MDS 暫存資料表**然後按**ENTER**。  
  
3.  連接**加入 MDS 所需的資料行**要**供應商資料寫入 MDS 暫存資料表**使用藍色連接器。  
  
4.  按兩下**供應商資料寫入 MDS 暫存資料表**中**資料流程** 索引標籤。  
  
5.  在  **OLE DB 目的地編輯器**對話方塊方塊中，請確定 **(local)。MDS** (或**localhost。MDS**) 選取**OLE DB 連接管理員**欄位。  
  
6.  選取**stg.Supplier_Leaf**從清單中的資料表**的資料表或檢視表名稱**。  
  
     ![OLEDB 目的地編輯器](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "OLEDB 目的地編輯器")  
  
7.  切換至**對應**頁面上，依序按一下**對應**左側功能表上。  
  
8.  地圖**輸入**並**目的地**下表所示的資料行。  
  
     ![OLEDB 目的地編輯器-對應](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "OLEDB 目的地編輯器-對應")  
  
9. 確認您使用 **_Output**之輸入資料行，不 **_Status**或是 **_Source**資料行。 **_Output**資料行包含 DQS 清理的輸出值。  
  
10. 按一下 [ **[確定]** 以關閉**OLE DB 目的地編輯器**] 對話方塊。  
  
11. 資料流程應該類似下圖。  
  
     ![完成資料流](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "完成資料流程")  
  
## <a name="next-step"></a>下一個步驟  
 [工作 14:將執行 SQL 工作，為 MDS 執行預存程序的控制流程](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
