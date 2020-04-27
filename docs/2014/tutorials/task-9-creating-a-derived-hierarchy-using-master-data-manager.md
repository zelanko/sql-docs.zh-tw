---
title: 工作9：使用主資料管理員建立衍生階層 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7cb2f12115e3fe743c49c2f7e69f765da4501ba2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489522"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>工作 9：使用主資料管理員建立衍生階層
  在這項工作中，您會使用主資料管理員建立衍生階層。 這個衍生階層衍生自**供應商**和**州**實體之間的網域屬性關聯性。  
  
1.  按一下頁面頂端的 [ **SQL Server 2012 Master Data Services** ]，切換至**主資料管理員**的主頁面。  
  
2.  按一下 [**管理**工作] 區段中的 [**系統管理**]。  
  
3.  將滑鼠停留在功能表列上的 [**管理**] 上，然後按一下 [**衍生**階層]。  
  
     ![管理功能表 - 已選取 [衍生階層]](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "管理功能表 - 已選取 [衍生階層]")  
  
4.  按一下工具列上的 **[加入衍生階層] （+）** 按鈕。  
  
     ![[加入衍生階層] 按鈕](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "[加入衍生階層] 按鈕")  
  
5.  針對 [衍生階層**名稱**] 輸入**SuppliersInState** 。  
  
6.  按一下工具列上的 [**儲存**] 按鈕。  
  
     ![[儲存衍生階層] 按鈕](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "[儲存衍生階層] 按鈕")  
  
7.  從可用的**層級**拖曳**供應商**： SuppliersInState 至**目前的層級： SuppliersInState**。  
  
     ![目前層級可用的實體和階層](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "目前層級可用的實體和階層")  
  
8.  從**State**可用的**層級拖曳狀態： SuppliersInState**到**目前的層級： SuppliersInState**。 畫面應具有**目前的層級**，如下圖所示。  
  
     ![衍生階層的目前層級和預覽](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "衍生階層的目前層級和預覽")  
  
9. 在 [**預覽**] 視窗中，展開 [ **NY {紐約}** ]，您應該會看到該狀態的一個供應商，如上圖所示。  
  
10. 按一下頁面頂端的 [ **SQL Server 2012 Master Data Services** ]，切換至**主資料管理員**的主頁面。  
  
11. 按一下 **[總管]**。  
  
12. 將滑鼠**停留在階層上，** 然後按一下 [**衍生： SuppliersInState**]。  
  
     ![階層 - [衍生:SuppliersInState] 功能表](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "階層 - [衍生:SuppliersInState] 功能表")  
  
13. 按一下**樹狀檢視**中的任何**狀態**節點，您應該會在右窗格中看到該狀態的供應商。  
  
     ![檔案總管中的衍生階層](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "檔案總管中的衍生階層")  
  
## <a name="next-step"></a>後續步驟  
 [第 5 課：使用 SSIS 將清理和比對自動化](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  
