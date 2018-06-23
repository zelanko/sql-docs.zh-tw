---
title: 工作 15： 建置和執行 SSIS 專案 |Microsoft 文件
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
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9a63fcf03591626d5b4c1351d5ce868ef7a9fb65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034686"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>工作 15：建立和執行 SSIS 專案
  在這項工作中，您會建立及執行 SSIS 專案。 如果您有 64 位元版本的電腦上安裝 Excel 2010，您應該設定的值**Run64BitRuntime**至**False**的 Excel 來源才能運作。  
  
1.  在**方案總管 中**視窗中，按一下 **專案**功能表，然後按一下  **CleanseAndCurateSuppliers 屬性**。  
  
2.  在**屬性**對話方塊方塊中，展開 **組態屬性**左邊，然後按一下 **偵錯**。  
  
3.  設定**Run64BitRuntime**至**False**。  
  
     ![CleanseAndCurateSuppliers 專案屬性](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "CleanseAndCurateSuppliers 專案屬性")  
  
4.  按一下**確定**關閉**屬性** 對話方塊。  
  
5.  按一下**建置**] 功能表，按一下 [**建立 CleanseAndCurateSuppliers**。 確定沒有任何建立錯誤。  
  
6.  按一下**偵錯**功能表列上按一下**開始偵錯**。  
  
7.  檢視中的郵件**進度**視窗並確認該封裝順利執行及結束。  
  
     ![產生進度視窗](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "產生進度視窗")  
  
     ![進度視窗中的最終狀態](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "進度視窗中的最終狀態")  
  
8.  按一下**偵錯**] 功能表，按一下 [**停止偵錯**停止偵錯工作階段。 如果封裝失敗，您應該啟用資料檢視器，並查看資料如何在元件之間流動。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 16： 驗證使用主資料管理員](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  