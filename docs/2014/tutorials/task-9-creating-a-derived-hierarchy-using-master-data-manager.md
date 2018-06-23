---
title: 工作 9： 建立衍生階層，使用主資料管理員 |Microsoft 文件
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 35584d33afac7a2a8f74abd013288a974cade512
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146637"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>工作 9：使用主資料管理員建立衍生階層
  在這項工作中，您會使用主資料管理員建立衍生階層。 這個衍生的階層衍生自網域屬性關聯性之間**供應商**和**狀態**實體。  
  
1.  切換至的主頁面**主資料管理員**按一下**SQL Server 2012 Master Data Services**頁面的頂端。  
  
2.  按一下**系統管理**中**系統管理工作**> 一節。  
  
3.  將滑鼠游標**管理**功能表列，然後按一下 **衍生階層**。  
  
     ![管理功能表-選取的衍生階層](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "管理功能表-選取的衍生階層")  
  
4.  按一下**加入衍生階層 （+）** 工具列上的按鈕。  
  
     ![加入衍生的階層 按鈕](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "加入衍生的階層 按鈕")  
  
5.  型別**SuppliersInState**如**衍生階層名稱**。  
  
6.  按一下**儲存**工具列上的按鈕。  
  
     ![儲存衍生階層 按鈕](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "儲存衍生階層 按鈕")  
  
7.  拖曳**供應商**從**可用層級： SuppliersInState**至**目前層級： SuppliersInState**。  
  
     ![可用的實體和階層，以便目前層級](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "可用的實體和目前層級的階層")  
  
8.  拖曳**狀態**從**可用層級： SuppliersInState**至**目前層級： SuppliersInState**。 畫面上應該有**目前層級**如下列圖片所示。  
  
     ![目前的層級和預覽衍生階層的](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "目前層級與預覽衍生階層")  
  
9. 在**預覽**視窗中，展開  **NY {New York}** 的上述影像中所示，您應該看到一家供應商處於該狀態。  
  
10. 切換至的主頁面**主資料管理員**按一下**SQL Server 2012 Master Data Services**頁面的頂端。  
  
11. 按一下 **[總管]**。  
  
12. 將滑鼠游標**階層**按一下**衍生： SuppliersInState**。  
  
     ![階層-[衍生： SuppliersInState] 功能表](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "階層-[衍生： SuppliersInState] 功能表")  
  
13. 按一下任何**狀態**節點**樹狀檢視**和您應該會看到在右窗格中該狀態供應商。  
  
     ![衍生階層總管 中](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "衍生階層總管中")  
  
## <a name="next-step"></a>下一個步驟  
 [第 5 課： 自動化清理和比對使用 SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  