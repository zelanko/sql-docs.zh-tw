---
title: 工作8：在 Excel 中為 State 實體加入新的值 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 831d0b504a65d485413772ee3711e689e29ee2a3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489701"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>工作 8：在 Excel 中為 State 實體新增值
  在這項工作中，您會在 Excel 中加入 State 實體的值，並將變更發行到 MDS 伺服器。  
  
1.  按一下底部的 [新增] 索引標籤，在 Excel 中加入**工作表**。  
  
     ![Excel - [新工作表] 索引標籤](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel - [新工作表] 索引標籤")  
  
2.  在**Excel**中，按一下功能表上的 [**主要資料**] 索引標籤，然後按一下功能區上的 [**顯示瀏覽器**]。  
  
3.  在 [**主要] 資料總管**中，選取 [適用于**模型**的**供應商**]。 您應該會在實體清單中看到兩個實體：**供應商**和**狀態**。  
  
4.  按兩下清單中的 [**狀態**]。 MDS 中**狀態**實體的所有成員都應該顯示在工作表中。  
  
5.  現在，在結尾加入包含下列值的資料列：適用于程式**代碼**的**名稱**和**NC**的**北卡羅萊納州**。 色彩編碼會區分任何新增/更新的記錄與其他記錄。  
  
     ![Excel-將北卡羅萊納州新增至州](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel-將北卡羅萊納州新增至州")  
  
6.  按一下功能區上的 [**發佈**]，將變更發佈至 MDS。  
  
     ![Excel - [主要資料] 索引標籤上的 [發佈] 按鈕](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel - [主要資料] 索引標籤上的 [發佈] 按鈕")  
  
7.  請注意，在 [**發行並批註**] 對話方塊中，已選取 [**針對所有變更使用相同的注釋**]。 您可以針對這裡的所有變更輸入單一註解。  
  
8.  選取 [**檢查變更並個別提供批註**] 選項，以提供每項變更的注釋（在此案例中，只有一個）。  
  
     ![Excel - [發行並註解] 對話方塊](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "Excel - [發行並註解] 對話方塊")  
  
9. 按一下 [**發佈**]，將資料發行至 MDS。  
  
10. 請注意，以**北卡羅萊納州**作為**狀態**的資料列的**色彩編碼**與現在的其他記錄相同。  
  
11. **選擇性：** 使用**主資料管理員**中的**Explorer** ，確認新的成員（NC）已加入至**State**實體。  
  
12. 在 Excel 中，以滑鼠右鍵按一下底部的**狀態**工作表，然後按一下 [**刪除**] 以刪除工作表。 刪除工作表並不會從 MDS 伺服器刪除任何資料。  
  
## <a name="next-step"></a>後續步驟  
 [工作 9：使用主資料管理員建立衍生階層](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  
