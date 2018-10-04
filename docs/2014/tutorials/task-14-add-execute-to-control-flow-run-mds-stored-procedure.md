---
title: 工作 14： 將執行 SQL 工作，為 MDS 執行預存程序的控制流程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9e2f62236d844a6ded850f33207bad9da082ce62
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177288"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>工作 14：將執行 SQL 工作加入到控制流程，為 MDS 執行預存程序
  將資料載入 MDS 的暫存資料表之後，您會執行與該資料表有關的預存程序，將暫存中的資料載入 MDS 資料庫中的適當資料表。 這個預存程序具有您必須傳遞的兩個必要參數：LogFlag 和 VersionName。 LogFlag 會指定暫存處理序期間所記錄的交易，而 VersionName 則代表模型的版本。 請參閱[暫存預存程序](http://msdn.microsoft.com/library/hh231028.aspx)如需詳細資訊。  
  
 在這項工作中，您會將「執行 SQL 工作」加入至控制流程來叫用預存程序，以便將暫存資料載入至適當的 MDS 資料表。  
  
1.  現在，請切換到**控制流程** 索引標籤。  
  
2.  拖放**執行 SQL 工作**從**SSIS 工具箱**來**控制流程** 索引標籤。  
  
3.  以滑鼠右鍵按一下**執行 SQL 工作**中**控制流程**索引標籤，然後按一下**重新命名**。 型別**觸發程序預存程序將資料載入至 MDS**然後按**ENTER**。  
  
4.  連接**接收、 清理、 比對和鑑定供應商資料**要**觸發程序預存程序將資料載入**使用綠色的連接子。  
  
     ![連接到執行 SQL 工作](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "連接到執行 SQL 工作")  
  
5.  使用**變數** 視窗中，使用下列設定加入兩個新的變數。 如果您看不見**變數**] 視窗中，按一下**SSIS**功能表列，然後按一下 [**變數**。  
  
    |名稱|資料類型|值|  
    |----------|---------------|-----------|  
    |LogFlag|Int32|1|  
    |VersionName|String|VERSION_1|  
  
     ![SSIS 變數視窗](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "SSIS 變數視窗")  
  
6.  按兩下**觸發程序將資料載入 MDS 的預存程序**。  
  
7.  在 **執行 SQL 工作編輯器**對話方塊中，選取 **(local)。MDS** (或**localhost。MDS**) 的**連線**。  
  
8.  型別**EXEC [stg]。 [udp_Supplier_Leaf]？，？，？** 針對**SQL 陳述式**。 您可以使用 SQL Server Management Studio 來驗證此名稱。  
  
     ![執行 SQL 編輯器對話方塊-一般設定](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "執行 SQL 編輯器對話方塊-一般設定")  
  
9. 按一下 **參數對應**從左側功能表上。  
  
10. 在 **參數對應**頁面上，按一下**新增**加入對應。 最大化視窗並調整資料行的大小，讓您可以適當地查看下拉式清單中的值。  
  
11. 選取  **user:: versionname**從下拉式清單**變數名稱**。  
  
12. 選取  **NVARCHAR** for**資料型別**。  
  
13. 型別**0** （零）**參數名稱**。  
  
14. 重複上述四個步驟來加入其他兩個變數。  
  
    |變數名稱|資料類型 (重要)|參數名稱|  
    |-------------------|-----------------------------|--------------------|  
    |User::LogFlag|LONG|1|  
    |User::BatchTag|NVARCHAR|2|  
  
     ![執行 SQL 工作編輯器-參數對應](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "執行 SQL 工作編輯器-參數對應")  
  
15. 按一下 [ **[確定]** 以關閉**執行 SQL 編輯器**] 對話方塊。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 15：建置及執行 SSIS 專案](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)  
  
  
