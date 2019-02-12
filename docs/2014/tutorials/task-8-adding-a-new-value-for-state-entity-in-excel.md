---
title: 工作 8:加入新的值為 State 實體，在 Excel 中 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 04ed80887a2a81a2179dcec423b9e22b3f9d43ef
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032029"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>工作 8:在 Excel 中為 State 實體加入新的值
  在這項工作中，您會在 Excel 中加入 State 實體的值，並將變更發行到 MDS 伺服器。  
  
1.  新增**工作表**在 Excel 中按一下底部的 [新增] 索引標籤。  
  
     ![Excel-新的工作表索引標籤](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel-新的工作表索引標籤")  
  
2.  在 [ **Excel**，按一下**Master Data**功能表上，索引標籤，然後按一下**顯示總管]** 功能區上。  
  
3.  在 **主資料總管**，選取**供應商**for**模型**。 您應該會在實體清單中看到兩個實體：**供應商**並**狀態**實體清單中。  
  
4.  按兩下**狀態**清單中。 所有成員**狀態**從 MDS 的實體應該顯示在工作表。  
  
5.  現在，請加入結尾包含以下值的資料列：**北卡羅萊納州**for**名稱**並**NC**如**程式碼**。 色彩編碼會區分任何新增/更新的記錄與其他記錄。  
  
     ![Excel-加入狀態的北卡羅萊納州](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel-北卡羅萊納州加入狀態")  
  
6.  按一下 **發佈**將變更發行到 MDS 功能區上。  
  
     ![Excel-[發行主要資料] 索引標籤上的按鈕](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel-[發行主要資料] 索引標籤上的按鈕")  
  
7.  上**發行並註解**對話方塊方塊中，注意**對所有變更使用相同的註解**已選取。 您可以針對這裡的所有變更輸入單一註解。  
  
8.  選取 **檢閱變更並個別提供註解**提供每個變更 （在此情況下，只有一個） 的註解的選項。  
  
     ![Excel-[發行並註解] 對話方塊](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "Excel-[發行並註解] 對話方塊")  
  
9. 按一下 **發佈**來將資料發行至 MDS。  
  
10. 請注意，**色彩編碼**使用資料列**北卡羅萊納州**作為**狀態**現已與其他記錄相同。  
  
11. **選擇性：** 確認新的成員 (NC) 已新增至**狀態**使用的實體**總管**中**主資料管理員**。  
  
12. 在 Excel 中，以滑鼠右鍵按一下**狀態**下方，然後按一下工作表**刪除**刪除工作表。 刪除工作表並不會從 MDS 伺服器刪除任何資料。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 9:建立衍生階層，使用主資料管理員](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  
