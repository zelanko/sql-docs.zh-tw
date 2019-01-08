---
title: 工作 3：從 Excel 檔案匯入定義域值 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 242e8309-1195-495b-9cd5-aa127748c185
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 16356826909edbde5218ad509af6864817a856c1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399201"
---
# <a name="task-3-importing-domain-values-from-an-excel-file"></a>工作 3：從 Excel 檔案匯入定義域值
  在這個工作中，您匯入的值**狀態**從工作表的 Excel 檔案的網域。  
  
1.  按一下 **狀態**中的網域**定義域清單**。  
  
2.  請確認**定義域值** 索引標籤為作用中的右窗格中。  
  
3.  在右窗格中，從工具列中，按一下**向下箭號**旁**匯入值**按鈕，然後按一下**從 Excel 匯入有效值**。  
  
     ![從 Excel 功能表匯入有效值](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-01.jpg "從 Excel 功能表匯入有效值")  
  
4.  按一下 **瀏覽**，選取**Suppliers.xls**，然後按一下**開啟**。  
  
5.  選取  **StatesToImport$** for**工作表**。  
  
     ![匯入定義域值 對話方塊](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-02.jpg "匯入定義域值 對話方塊")  
  
6.  按一下 [ **[確定]** 以關閉**匯入定義域值**] 對話方塊。 您應該會看到您已匯入到清單中的所有州別名稱。 請注意，**只顯示新**匯入後會自動選取選項。 當您匯入值，您沒有看到清單中的舊值，是因為匯入之後，會自動啟用此選項。 若要查看所有值，請清除核取方塊。 如果您重新匯入相同的一組值，任何值都不會匯入，因為它們已經存在於定義域中。  
  
     ![在 定義域值上顯示只有新的核取方塊](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-03.jpg "只有新的核取方塊顯示定義域值")  
  
## <a name="next-step"></a>下一個步驟  
 [工作 4:設定定義域規則](../../2014/tutorials/task-4-setting-domain-rules.md)  
  
  
