---
title: 工作2：將 Excel 資料行對應到 DQS 定義域 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f347cc92-950f-4021-b7af-393640dfe821
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 29d45e06dcd3e67af3abbc6b356d44877e40f46b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484699"
---
# <a name="task-2-mapping-excel-columns-to-dqs-domains"></a>工作 2：將 Excel 資料行對應到 DQS 定義域
    
1.  在 [對應] **** 頁面上，針對 [資料來源] **** 選取 [Excel 檔案] ****。  
  
2.  按一下 **[流覽]**，選取 [**供應商 .xlsx**]，然後按一下 [**開啟**]。  
  
3.  針對**工作表**選取 [ **IncomingSuppliers $** ]。  
  
4.  對應資料行，如下表和螢幕擷取畫面所示。 建立**狀態**網域的對應時，請按一下工具列上位於清單正上方的 [**加入資料行對應**] 按鈕。  
  
    > [!TIP]  
    >  您不會使用**供應商識別碼**資料行/網域進行清理。 您稍後會在比對活動中使用**供應商識別碼**網域。  
  
    |Excel 資料行|DQS 定義域|  
    |------------------|----------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|連絡人電子郵件|  
    |[地址行]|[地址行]|  
    |City|City|  
    |State|State|  
    |國家/地區（按一下 [ **+] （加入資料行對應）** 工具列以加入資料列）|Country|  
    |Zip Code|Zip|  
  
     ![將 Excel 資料行對應到定義域](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-01.jpg "將 Excel 資料行對應到定義域")  
  
5.  當您已對應「**位址驗證**」複合定義域中的所有個別網域時，複合定義域會自動參與清理程式。 按一下 [**視圖/選取複合定義域**] 按鈕，以查看是否已自動選取 [**位址驗證**] 複合定義域，然後按一下 **[確定]**。  
  
     ![[檢視/選取複合定義域] 對話方塊](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-02.jpg "[檢視/選取複合定義域] 對話方塊")  
  
6.  按 **[下一步]** 切換至 [**清理**] 頁面。  
  
## <a name="next-step"></a>後續步驟  
 [工作 3：針對供應商知識庫清理資料](../../2014/tutorials/task-3-cleansing-data-against-the-suppliers-knowledge-base.md)  
  
  
