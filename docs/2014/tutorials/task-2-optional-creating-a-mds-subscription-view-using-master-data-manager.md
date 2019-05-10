---
title: 工作 2 (選擇性)：建立 MDS 訂閱檢視，使用主資料管理員 |Microsoft Docs
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
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484718"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>工作 2 (選擇性)：使用主資料管理員建立 MDS 訂閱檢視
  在這個工作中，您會建立訂閱檢視，公開**供應商**中的實體**供應商**模型到其他應用程式。 您不會在目前的教學課程版本中使用這個檢視。  
  
1.  切換至的主頁面**主資料管理員**([http://localhost/MDS](http://localhost/MDS))，即可**SQL Server 2012 Master Data Services**頂端。  
  
2.  按一下 **整合管理**。  
  
3.  按一下 **建立檢視表**功能表列上。  
  
     ![加入新的訂用帳戶檢視 按鈕](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "新增新的訂用帳戶檢視 按鈕")  
  
4.  按一下 [ **+ （加號）** 建立訂閱檢視] 工具列上的圖示。  
  
5.  在 **建立訂閱檢視**窗格中，輸入**供應商**for**訂用帳戶檢視表名稱**。  
  
6.  選取 **供應商**for**模型**。  
  
7.  選取  **VERSION_1** for**版本**。  
  
8.  選取 **供應商**for**實體**。  
  
9. 選取 **分葉成員**for**格式**。  
  
     ![儲存訂閱檢視 按鈕](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "儲存訂閱檢視 按鈕")  
  
10. 按一下 [**儲存**儲存訂閱檢視] 工具列上。 這個動作會建立名為 SQL Server 中的檢視**供應商**。 您可以使用 SQL Server Management Studio (SSMS) 來驗證。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 3&#40;選擇性&#41;:檢閱訂閱檢視](task-3-optional-reviewing-the-subscription-views.md)  
  
  
