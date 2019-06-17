---
title: 工作 17：檢閱 SSIS 封裝的 DQS 清理專案建立 |Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484717"
---
# <a name="task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package"></a>工作 17：檢閱 SSIS 封裝所建立的 DQS 清理專案
  在這項工作中，您會開啟 DQS 用戶端中的 SSIS 封裝所建立的 DQS 專案、檢閱清理程序的結果，並選擇性地執行互動式清理及匯出結果。  
  
1.  啟動**Data Quality Client**。  
  
2.  按一下 **活動監控**中**管理**窗格。  
  
3.  排序依據清單**活動開始時間**以查看最新的記錄。  
  
4.  請注意，您會看到以下列格式的專案名稱：**CleanseAndCurate.Cleanse Supplier Data.GUID**。  
  
     ![DQS 清理專案建立的 SSIS 封裝](../../2014/tutorials/media/et-reviewingdqscpcreatedbythessispackage.jpg "SSIS 封裝所建立的 DQS 清理專案")  
  
5.  請注意，中的值**為使用**欄位是**Active**。  
  
6.  按一下 [ **Profiler** ] 索引標籤以查看 SSIS 封裝執行清理活動的分析工具統計資料的下方窗格中。  
  
7.  按一下 **關閉** 以關閉**管理**螢幕。  
  
8.  中的主頁面**DQS 用戶端**，按一下**開啟資料品質專案**中**資料品質專案**窗格。  
  
9. 在專案清單中，選取 SSIS DQS 清理元件所建立的專案。 專案的名稱應該採用格式：**CleanseAndCurate.Cleanse Supplier Data.GUID (紅色）** 。 您可能需要根據清單排序**建立日期**資料行並尋找最新的記錄。  
  
10. 按一下 [下一步]  。  
  
11. **管理和檢視結果**頁面應該很熟悉從您稍早在本教學課程中執行互動式清理。  
  
12. 檢閱清理結果。 您也可以執行互動式清理，並在下一頁將結果匯出到 Excel 檔案或資料庫。  
  
13. 按一下 [下一步]  。 在此**匯出** 頁面上，您可以將結果匯出到 excel 檔案中，CSV 檔案，或 SQL database。  
  
14. 按一下 **完成**完成的活動。  
  
15. 中的主頁面**DQS 用戶端**，按一下**活動監控**中**管理**窗格。  
  
16. 請注意，值**IsActive**欄位為**結束**現在。  
  
## <a name="next-step"></a>下一個步驟  
 [結論](../../2014/tutorials/conclusion.md)  
  
  
