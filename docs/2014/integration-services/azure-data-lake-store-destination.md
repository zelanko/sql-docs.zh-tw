---
title: Azure Data Lake Store 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSDEST.F1
- SQL11.DTS.DESIGNER.AFPADLSDEST.F1
ms.assetid: d0e86032-2a6b-48b2-898f-e94328474fde
caps.latest.revision: 5
author: yualan
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7ca00d765a0279a70f0758a917ce51343e7be362
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37272204"
---
# <a name="azure-data-lake-store-destination"></a>Azure Data Lake Store 目的地
  **Azure Data Lake Store 目的地** 元件可讓 SSIS 套件將資料寫入 Azure Data Lake Store。 支援的檔案格式為文字、Avro 和 ORC。 
  
## <a name="configure-the-azure-data-lake-store-destination"></a>設定 Azure Data Lake Store 目的地 

1. 將 **Azure Data Lake Store 目的地** 拖放到資料流程設計師，然後在上面按兩下以查看編輯器。  

2.  在 [Azure Data Lake Store 連線管理員]  欄位指定現有的 Azure Data Lake Store 連線管理員，或建立參考 Azure Data Lake Store 服務的新連線管理員。  
  
    1.  在 [檔案路徑]  欄位指定想要寫入資料的檔案名稱。 如果此檔案已經存在，即會覆寫其內容。  
  
    2.  在 [檔案格式]  欄位指定想要使用的檔案格式。  
  
        檔案格式若為文字，則您必須指定 [資料行分隔符號字元]  值。 若檔案中第一個資料列包含資料行名稱，請選取 [第一個資料列的資料行名稱]  。  

        如果使用 ORC 檔案格式，您需要安裝對應平台的 JRE。 
  
3.  指定連接資訊後，請切換至 [資料行]  頁面，將來源資料行對應至 SSIS 資料流程的目的地資料行。  
