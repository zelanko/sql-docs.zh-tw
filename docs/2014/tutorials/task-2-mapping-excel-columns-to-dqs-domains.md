---
title: 工作 2： 將 Excel 資料行對應到 DQS 定義域 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f347cc92-950f-4021-b7af-393640dfe821
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ff48d56555d3eca2bbcb961d753a47d8db38c69e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144635"
---
# <a name="task-2-mapping-excel-columns-to-dqs-domains"></a>工作 2：將 Excel 資料行對應到 DQS 定義域
    
1.  在 [對應]  頁面上，針對 [資料來源]  選取 [Excel 檔案] 。  
  
2.  按一下**瀏覽**，選取**Suppliers.xlsx**，然後按一下**開啟**。  
  
3.  選取**IncomingSuppliers$** 如**工作表**。  
  
4.  對應資料行，如下表和螢幕擷取畫面所示。 建立對應時**狀態**網域中，按一下 **加入資料行對應**位於清單正上方的工具列上的按鈕。  
  
    > [!TIP]  
    >  您不使用**Supplier ID**資料行/定義域進行清理。 您將使用**Supplier ID**稍後的比對活動的網域。  
  
    |Excel 資料行|DQS 定義域|  
    |------------------|----------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Contact Email|  
    |[地址行]|[地址行]|  
    |[縣/市]|[縣/市]|  
    |State|State|  
    |國家/地區 (按一下 **+ （加入資料行對應）** 工具列來加入一個資料列)|Country|  
    |Zip Code|[郵遞區號]|  
  
     ![網域的 Excel 資料行對應](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-01.jpg "至網域的 Excel 資料行對應")  
  
5.  因為我們已經對應中的個別定義域**地址驗證**複合定義域的複合定義域會自動參與清理程序。 按一下**檢視/選取複合定義域**按鈕，查看**地址驗證**複合定義域已自動選取，然後**確定**。  
  
     ![檢視/選取複合定義域 對話方塊](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-02.jpg "檢視/選取複合定義域 對話方塊")  
  
6.  按一下**下一步**切換至**清理**頁面。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 3： 針對清理資料供應商知識庫](../../2014/tutorials/task-3-cleansing-data-against-the-suppliers-knowledge-base.md)  
  
  