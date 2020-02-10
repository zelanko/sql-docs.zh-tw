---
title: 工作2（選擇性）：使用主資料管理員建立 MDS 訂閱視圖 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e6cbed42d059714dde1c82dbb50edf8ccc1dd65b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484718"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>工作 2 (選擇性)：使用主資料管理員建立 MDS 訂閱檢視
  在這項工作中，您會建立訂閱視圖，將**供應商**模型中的**供應商**實體公開給其他應用程式。 您不會在目前的教學課程版本中使用這個檢視。  
  
1.  按一下頂端的 [ **SQL Server 2012** ] Master Data Services[http://localhost/MDS](http://localhost/MDS)，切換到**主資料管理員**的主頁面（）。  
  
2.  按一下 [**整合管理**]。  
  
3.  按一下功能表列上的 [**建立視圖**]。  
  
     ![[加入新的訂閱檢視] 按鈕](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "[加入新的訂閱檢視] 按鈕")  
  
4.  按一下工具列上的 **[+ （加號）** ] 圖示，以建立訂用帳戶視圖。  
  
5.  在 [**建立訂**用帳戶] 視圖窗格中，輸入**供應商**的**訂閱視圖名稱**。  
  
6.  選取 [適用于**模型**的**供應商**]。  
  
7.  針對 [**版本**] 選取 [ **VERSION_1** ]。  
  
8.  選取 [**實體**的**供應商**]。  
  
9. 選取 [分**葉成員**] 做為 [**格式**]。  
  
     ![[儲存訂閱檢視] 按鈕](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "[儲存訂閱檢視] 按鈕")  
  
10. 按一下工具列上的 [**儲存**] 來儲存訂閱視圖。 此動作會在名為**供應商**的 SQL Server 中建立一個視圖。 您可以使用 SQL Server Management Studio (SSMS) 來驗證。  
  
## <a name="next-step"></a>後續步驟  
 [工作 3 &#40;選擇性&#41;：審查訂閱視圖](task-3-optional-reviewing-the-subscription-views.md)  
  
  
