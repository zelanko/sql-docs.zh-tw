---
title: "Azure Data Lake Store 來源 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSSRC.F1
- sql14.dts.designer.afpadlssrc.f1
ms.assetid: f9c3311f-7316-48d6-bf10-d810e70b4304
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: da63d0250bc374ab93d3c8df8375837aabac7223
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="azure-data-lake-store-source"></a>Azure Data Lake Store 來源
  **Azure Data Lake Store 來源** 元件可讓 SSIS 套件從 Azure Data Lake Store 讀取資料。 支援的檔案格式為文字和 Avro。
  
 **Azure Data Lake Store 來源**是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。  
  
>   [!NOTE]
> 為確保 Azure Data Lake Store 連線管理員及使用它的元件 (即 Azure Data Lake Store 來源及 Azure Data Lake Store 目的地) 能夠連接服務，請務必從 [這裡](https://www.microsoft.com/download/details.aspx?id=49492)下載最新版的 Azure Feature Pack。 
  
## <a name="configure-the-azure-data-lake-store-source"></a>設定 Azure Data Lake Store 來源
 1. 若要查看 Azure Data Lake Store 來源的編輯器，可在資料流程設計師上拖放 **Azure Data Lake Store 來源** ，並連按兩下以開啟編輯器。  
  
2.  在 [Azure Data Lake Store 連線管理員]  欄位指定現有的 Azure Data Lake Store 連線管理員，或建立參考 Azure Data Lake Store 服務的新連線管理員。  
  
    1.  在 [檔案路徑]  欄位指定 Azure Data Lake Store 來源檔案的檔案路徑。   
  
    2.  在 [檔案格式]  欄位指定來源檔案的檔案格式。  
  
        檔案格式若為文字，則您必須指定 [資料行分隔符號字元]  值。 若檔案中第一個資料列包含資料行名稱，請選取 [第一個資料列的資料行名稱]  。  
  
3.  指定連接資訊後，請切換至 [資料行]  頁面，將來源資料行對應至 SSIS 資料流程的目的地資料行。   
