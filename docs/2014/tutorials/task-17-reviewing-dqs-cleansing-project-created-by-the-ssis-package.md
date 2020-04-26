---
title: 工作17：查看 SSIS 封裝所建立的 DQS 清理專案 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fc6cc258-72f5-4593-8edb-9f5bc66de9db
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 285eae7ea20d5919fa73bd0d514c755fe73d9de0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484717"
---
# <a name="task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package"></a>工作 17：檢閱 SSIS 封裝所建立的 DQS 清理專案
  在這項工作中，您會開啟 DQS 用戶端中的 SSIS 封裝所建立的 DQS 專案、檢閱清理程序的結果，並選擇性地執行互動式清理及匯出結果。  
  
1.  啟動**Data Quality Client**。  
  
2.  按一下 [系統**管理**] 窗格中的 [**活動監控**]。  
  
3.  依據 [**活動開始時間**] 排序清單，以查看最新的記錄。  
  
4.  請注意，您會看到專案的名稱，格式如下： **cleanseandcurate.cleanse supplier data.guid。清理供應商資料. GUID**。  
  
     ![SSIS 封裝建立的 DQS 清理專案](../../2014/tutorials/media/et-reviewingdqscpcreatedbythessispackage.jpg "SSIS 封裝建立的 DQS 清理專案")  
  
5.  請注意，[ **Is active** ] 欄位中的值為 [**作用中]。**  
  
6.  按一下**底部**窗格中的 [分析工具] 索引標籤，以查看 SSIS 封裝執行之清理活動的 Profiler 統計資料。  
  
7.  按一下 [**關閉**] 以關閉 [**管理**] 畫面。  
  
8.  在**DQS 用戶端**的主頁面中，按一下 [**資料品質**專案] 窗格中的 [**開啟資料品質專案**]。  
  
9. 在專案清單中，選取 SSIS DQS 清理元件所建立的專案。 專案的名稱應採用下列格式： **cleanseandcurate.cleanse supplier data.guid。清理供應商資料。 GUID （以紅色表示）**。 您可能需要根據 [**建立日期] 資料**行來排序清單，並尋找最新的記錄。  
  
10. 按 [下一步]  。  
  
11. 從您稍早在本教學課程中進行的互動式清理，您應該不熟悉 [**管理] 和 [查看結果**] 頁面。  
  
12. 檢閱清理結果。 您也可以執行互動式清理，並在下一頁將結果匯出到 Excel 檔案或資料庫。  
  
13. 按 [下一步]  。 在此**匯出**頁面中，您可以將結果匯出至 excel 檔案、CSV 檔案或 SQL 資料庫。  
  
14. 按一下 **[完成]** 以完成活動。  
  
15. 在**DQS 用戶端**的主頁面中，按一下 [系統**管理**] 窗格中的 [**活動監控**]。  
  
16. 請注意，專案的 [ **IsActive** ] 欄位的值現在已**結束**。  
  
## <a name="next-step"></a>後續步驟  
 [結論](../../2014/tutorials/conclusion.md)  
  
  
