---
title: 工作 5： 從 Excel 建立的網域屬性 |Microsoft 文件
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
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5e7a8dda16d8f513b2c4b07b9f41712be806b8a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131613"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>工作 5：從 Excel 建立定義域屬性
  在這項工作，您將轉換**狀態**屬性**供應商**與實體**網域型屬性**。 設定網域為基礎的策略，並將它發行到 MDS，名為新的實體的 State 屬性之後**狀態**將具有資料行中的所有值的 MDS 伺服器上建立和**狀態**屬性**供應商**實體會填入值，從**狀態**實體。 現在，**供應商**模型應該有兩個實體：**供應商**和**狀態**其中**狀態**屬性**供應商**實體是取決於網域型屬性**狀態**實體。  
  
1.  切換至**Excel**視窗有**Cleansed and Matched Suppliers.xlsx**開啟。  
  
2.  按一下**重新整理**從 MDS 取得最新的更新功能區上的按鈕。 您應該看到兩筆記錄，如果您已執行選擇性**工作 4**。  
  
3.  按一下資料行名稱**狀態**(儲存格**I1**) 中**標頭資料列**。  
  
     ![Excel-[屬性內容] 按鈕](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel-[屬性內容] 按鈕")  
  
4.  按一下**屬性**功能區上。  
  
5.  在**屬性**對話方塊中，選取**Constrained 清單 （以網域為基礎）** 如**屬性類型**。  
  
6.  型別**狀態**如**新實體名稱**按一下**確定**。  
  
     ![Excel-[屬性內容] 對話方塊中](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel-[屬性內容] 對話方塊")  
  
7.  現在，在 Excel 中，您應該會看到**向下箭號**當您按一下中的任何值**狀態**資料行。 您可以視需要使用下拉式清單變更此值。  
  
     ![Excel-下拉式清單具有狀態](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel-下拉式清單中的狀態")  
  
## <a name="next-step"></a>下一個步驟  
 [工作 6： 確認已建立使用主資料管理員的網域屬性](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  