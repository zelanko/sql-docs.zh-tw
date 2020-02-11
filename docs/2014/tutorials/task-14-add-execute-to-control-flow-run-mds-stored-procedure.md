---
title: 工作14：將執行 SQL 工作新增至控制流程，以執行 MDS 的預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3fe1eb6032d9d550b36252e16eee51c98c5d2384
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65477077"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>工作 14：將執行 SQL 工作加入到控制流程，為 MDS 執行預存程序
  將資料載入 MDS 的暫存資料表之後，您會執行與該資料表有關的預存程序，將暫存中的資料載入 MDS 資料庫中的適當資料表。 這個預存程序具有您必須傳遞的兩個必要參數：LogFlag 和 VersionName。 LogFlag 會指定暫存處理序期間所記錄的交易，而 VersionName 則代表模型的版本。 如需詳細資訊，請參閱[分段預存](https://msdn.microsoft.com/library/hh231028.aspx)程式主題。  
  
 在這項工作中，您會將「執行 SQL 工作」加入至控制流程來叫用預存程序，以便將暫存資料載入至適當的 MDS 資料表。  
  
1.  現在，切換到 [**控制流程**] 索引標籤。  
  
2.  從 [ **SSIS 工具箱**] 將 [**執行 SQL**工作] 拖放至 [**控制流程**] 索引標籤。  
  
3.  以滑鼠右鍵按一下 [**控制流程**] 索引標籤中的 [**執行 SQL**工作]，然後按一下 [**重新命名**] 輸入**觸發程式預存程式，將資料載入 MDS** ，然後按**enter**。  
  
4.  連接**接收、清理、比對和策展供應商資料**，以使用綠色連接器來**觸發預存程式來載入資料**。  
  
     ![連接至「執行 SQL」工作](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "連接至「執行 SQL」工作")  
  
5.  使用 [**變數**] 視窗，使用下列設定加入兩個新的變數。 如果您看不到 [**變數**] 視窗，請按一下功能表列上的 [ **SSIS** ]，然後按一下 [**變數**]。  
  
    |名稱|資料類型|值|  
    |----------|---------------|-----------|  
    |LogFlag|Int32|1|  
    |VersionName|String|VERSION_1|  
  
     ![SSIS 變數視窗](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "SSIS 變數視窗")  
  
6.  按兩下 [**觸發預存程式]，將資料載入 MDS**。  
  
7.  在 [**執行 SQL 工作編輯器**] 對話方塊中，選取 [ **（本機）]。MDS** （或**localhost。MDS**）進行**連接**。  
  
8.  輸入**EXEC [stg.<]. [udp_Supplier_Leaf]?,?,?** 適用于**SQL 語句**。 您可以使用 SQL Server Management Studio 來驗證此名稱。  
  
     ![執行 SQL 編輯器對話方塊 - 一般設定](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "執行 SQL 編輯器對話方塊 - 一般設定")  
  
9. 按一下左側功能表中的 [**參數對應**]。  
  
10. 在 [**參數對應**] 頁面上，按一下 [**新增**] 以新增對應。 最大化視窗並調整資料行的大小，讓您可以適當地查看下拉式清單中的值。  
  
11. 從 [**變數名稱**] 的下拉式清單中，選取 [ **User：： VersionName** ]。  
  
12. 針對 [**資料類型**] 選取 [ **NVARCHAR** ]。  
  
13. 為 [**參數名稱**] 輸入**0** （零）。  
  
14. 重複上述四個步驟來加入其他兩個變數。  
  
    |變數名稱|資料類型 (重要)|參數名稱|  
    |-------------------|-----------------------------|--------------------|  
    |User::LogFlag|LONG|1|  
    |User::BatchTag|NVARCHAR|2|  
  
     ![執行 SQL 工作編輯器 - 參數對應](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "執行 SQL 工作編輯器 - 參數對應")  
  
15. 按一下 **[確定]** 以關閉 [**執行 SQL 編輯器**] 對話方塊。  
  
## <a name="next-step"></a>後續步驟  
 [工作 15：建立和執行 SSIS 專案](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)  
  
  
