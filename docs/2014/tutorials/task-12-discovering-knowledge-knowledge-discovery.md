---
title: 工作 12：探索知識 （知識探索） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: dd80a8e6-1e41-4c49-9898-02b1d2505a10
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6dd54475ee63b2f6ef5e1b56b94c11aafd5996ff
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484687"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>工作 12：探索知識 (知識探索)
  在這個工作中，您會執行**知識探索**上的活動**Supplier ID**並**Supplier Name**網域。 在此案例中，知識探索程序主要會匯入這兩個定義域的值。  
  
 在本教學課程中，您會從頭開始建立知識庫。 您也可以藉由執行知識探索活動來開始建立知識庫。 當您按一下 **建立知識庫**在主頁面中，DQS 用戶端會帶您前往與頁面**定義域管理**選取活動的活動。 您可以變更**活動**要**知識探索**，然後在下一個頁面中您可以建立網域知識探索程序的一部分。 請參閱[Perform Knowledge Discovery](https://msdn.microsoft.com/library/hh510398.aspx)如需詳細資訊。  
  
1.  在 DQS 用戶端的主頁面中**最新的知識庫**區段中，按一下**向右箭號**旁**供應商**知識庫，然後按一下 **知識探索**。 或者，您可以按一下**開啟知識庫**，選取**供應商**從**知識庫清單**，選取**知識探索**作為**活動**然後按一下**下一步**。  
  
     ![知識探索 功能表，在主要頁面](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "知識探索 功能表，在主要頁面")  
  
2.  選取  **Excel 檔案**for**資料來源**。  
  
3.  按一下 **瀏覽**，瀏覽並選取**Suppliers.xls**，然後按一下**開啟**。  
  
4.  選取  **Suppliers for Discovery** for**工作表**。  
  
5.  在 **對應**區段中，對應**SupplierID**從資料行**Excel**檔案**Supplier ID**網域和**Supplier Name**資料行**Supplier Name**使用的網域**下拉式清單**。 Excel 檔案有範例資料**Supplier ID**並**Supplier Name**網域。 在探索程序中，您可以選取要探索值的定義域。 您可以在此頁面建立定義域，然後將來源資料行對應到這些定義域。 在知識探索活動期間建立定義域是可能發生的狀況 (而不是在定義域管理活動期間建立定義域)。  
  
     ![[對應] 頁面的探索程序](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "對應的探索程序的頁面")  
  
6.  按一下 [**下一步]** 轉為**Discover**頁面。  
  
7.  在  **Discover**頁面上，按一下**開始**開始探索程序。 資料行執行探索**SupplierID**並**Supplier Name**中**Suppliers.xls**檔案。 **Supplier ID**並**Supplier Name**定義域應該填入從探索發現的知識。  
  
     ![[探索] 頁面的探索程序](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "探索的探索程序的頁面")  
  
8.  分析完成後，請檢閱**來源統計資料**中**Profiler 索引標籤**在頁面底部。 請注意，10 筆新記錄總計 20 個值 (**SupplierID**並**Supplier Name**值**Excel 工作表**) 所探索到。 您也會看到有多少新的值、唯一的值、新增且唯一的值及有效的值。 在右邊的清單方塊中，您可以查看與探索程序有關之每個定義域的更多詳細資料。 如果您將滑鼠停留在狀態列的 [完整性] 資料行上方，您可以看到資料行的來源是否有任何遺漏的值。  
  
     ![知識探索結果](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "知識探索結果")  
  
9. 按一下 **下一步**轉為**管理定義域值**頁面。  
  
10. 在 **管理定義域值**頁面上，按一下**Supplier Name**網域的網域清單。  
  
11. 在右窗格中，以滑鼠右鍵按一下**Lazy Country Storex** （請注意 'x' 結束），然後選取**Lazy Country Store**。 在針對此定義域執行拼字檢查之後，DQS 會建議這項變更。 根據預設，您建立的定義域會啟用拼字檢查。  
  
     ![更正的供應商名稱-Lazy Country Store](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "正確供應商名稱-Lazy Country Store")  
  
12. 在 [定義域值] 清單中，確認值**Lazy Country Storex**設定為錯誤 (紅色**X**標記) 與**Lazy Country Store**為更正，且**Lazy Country Store**也會加入做為有效的值。  
  
     ![定義域值，並更正為 值](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "網域值，並更正為 值")  
  
13. 按一下 **[完成]**。  
  
14. 在 [ **SQL Server Data Quality Services** ] 對話方塊中，按一下**發佈**。  
  
15. 按一下 **確定**成功訊息方塊上。  
  
     您已經完成教學課程的第一課。  
  
## <a name="next-step"></a>下一個步驟  
 [第 2 課：使用供應商知識庫清理供應商資料](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  
