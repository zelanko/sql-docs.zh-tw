---
title: 任務 2(選擇性的):使用主資料管理員建立 MDS 訂閱檢視 |微軟文件
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
ms.openlocfilehash: cc923792adc3fefb5ebaab9e225169648394c71f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484708"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>工作 2 (選擇性)：使用主資料管理員建立 MDS 訂閱檢視
  在此任務中,您將創建一個訂閱檢視,以將**供應商模型中的供應商**實體公開給其他應用程式。 **Supplier** 您不會在目前的教學課程版本中使用這個檢視。  
  
1.  按一下頂部的**SQL Server 2012 主資料服務**,切換`http://localhost/MDS`到**主資料管理員**( ) 的主頁。  
  
2.  點選**的管理**。  
  
3.  按一下選單欄上的 **「創建檢視**」。  
  
     ![[加入新的訂閱檢視] 按鈕](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "[加入新的訂閱檢視] 按鈕")  
  
4.  按一下工具列上的 **+(加號)** 圖示以創建訂閱檢視。  
  
5.  在 **「建立訂閱檢視」** 窗格中, 鍵入**訂閱檢視名稱****的供應商**。  
  
6.  為**模型**選擇**供應商**。  
  
7.  選擇**版本****VERSION_1。**  
  
8.  為**實體**選擇**供應商**。  
  
9. 為 **'格式****' 選擇「葉」 成員**。  
  
     ![[儲存訂閱檢視] 按鈕](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "[儲存訂閱檢視] 按鈕")  
  
10. 按一下工具列上的 **「儲存**」以保存訂閱檢視。 此操作在 SQL Server 中建立名為 **「供應商」的**檢視。 您可以使用 SQL Server Management Studio (SSMS) 來驗證。  
  
## <a name="next-step"></a>後續步驟  
 [工作 3 &#40;可选&#41;:查看訂閱檢視](task-3-optional-reviewing-the-subscription-views.md)  
  
  
