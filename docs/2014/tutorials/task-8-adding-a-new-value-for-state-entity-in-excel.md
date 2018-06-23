---
title: 工作 8： 加入新的值為 State 實體，在 Excel 中 |Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: db2eaccd4d9b344cbc1b7c25b6fec940ff9c77a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135518"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>工作 8：在 Excel 中為 State 實體加入新的值
  在這項工作中，您會在 Excel 中加入 State 實體的值，並將變更發行到 MDS 伺服器。  
  
1.  新增**工作表**在 Excel 中按一下新的索引標籤底部。  
  
     ![Excel-新工作表索引標籤](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel-新工作表索引標籤")  
  
2.  在**Excel**，按一下 **主要資料**功能表上，索引標籤，然後按一下 **顯示總管**功能區上。  
  
3.  在**主資料總管**，選取**供應商**如**模型**。 您應該會看到兩個實體：**供應商**和**狀態**在實體清單中。  
  
4.  按兩下**狀態**清單中。 所有成員**狀態**從 MDS 的實體應該顯示在工作表。  
  
5.  現在，加入一個資料列結尾包含下列值：**北卡羅來那州**如**名稱**和**NC**如**程式碼**。 色彩編碼會區分任何新增/更新的記錄與其他記錄。  
  
     ![Excel-North Carolina 加入狀態](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel-North Carolina 加入狀態")  
  
6.  按一下**發行**將變更發行到 MDS 功能區上。  
  
     ![Excel-[發行主要資料] 索引標籤上的按鈕](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel-[發行主要資料] 索引標籤上的按鈕")  
  
7.  在**發行並註解**對話方塊方塊中，請注意，**所有變更使用相同的註解**已選取。 您可以針對這裡的所有變更輸入單一註解。  
  
8.  選取**檢閱變更並個別提供註解**選項，即可提供註解的每個變更 （在此情況下，只有一個）。  
  
     ![Excel-發行並註解對話方塊](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "Excel-[發行並註解] 對話方塊")  
  
9. 按一下**發行**將資料發佈至 MDS。  
  
10. 請注意，**色彩編碼**之資料列的**北卡羅來那州**為**狀態**現在是與其他記錄相同。  
  
11. **選擇性：** 確認新的成員 (NC) 加入至**狀態**實體使用**總管**中**主資料管理員**。  
  
12. 在 Excel 中，以滑鼠右鍵按一下**狀態**工作表底部，然後按一下**刪除**刪除工作表。 刪除工作表並不會從 MDS 伺服器刪除任何資料。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 9： 建立衍生階層，使用主資料管理員](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  