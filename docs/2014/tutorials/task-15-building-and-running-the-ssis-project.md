---
title: 工作15：建立和執行 SSIS 專案 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
ms.author: lle
author: lrtoyou1223
ms.openlocfilehash: 50b313f63ae434a96d6c0e38f3c8b600914c806d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66822990"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>工作 15：建置及執行 SSIS 專案

  在這項工作中，您會建立及執行 SSIS 專案。 如果您的電腦上已安裝64位版本的 Excel 2010，則您應該將**Run64BitRuntime**的值設定為**False** ，excel 來源才能正常執行。  
  
1.  在 [**方案總管**] 視窗中，按一下功能表上的 [**專案**]，然後按一下 [ **CleanseAndCurateSuppliers 屬性**]。  
  
2.  在 [**屬性**] 對話方塊中，展開左側的 [設定**屬性**]，然後按一下 [**調試**]。  
  
3.  將**Run64BitRuntime**設定為**False**。  
  
     ![CleanseAndCurateSuppliers 專案屬性](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "CleanseAndCurateSuppliers 專案屬性")  
  
4.  按一下 [確定]**** 以關閉 [內容]**** 對話方塊。  
  
5.  按一下功能表列上的 [**建立**]，然後按一下 [**建立 CleanseAndCurateSuppliers**]。 確定沒有任何建立錯誤。  
  
6.  按一下功能表列上的 [ **Debug** ]，然後按一下 [**開始調試**]。  
  
7.  查看 [**進度**] 視窗中的訊息，並確認已成功執行和結束封裝。  
  
     ![進度視窗中的 [結果]](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "進度視窗中的 [結果]")  
  
     ![進度視窗中的 [最後狀態]](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "進度視窗中的 [最後狀態]")  
  
8.  按一下功能表列上的 [ **Debug** ]，然後按一下 [**停止調試**] 以停止調試進程。 如果封裝失敗，您應該啟用資料檢視器，並查看資料如何在元件之間流動。  
  
## <a name="next-step"></a>後續步驟  
 [工作 16：使用主資料管理員驗證](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  
