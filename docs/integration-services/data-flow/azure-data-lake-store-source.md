---
title: Azure Data Lake Store 來源 | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSSRC.F1
- sql14.dts.designer.afpadlssrc.f1
ms.assetid: f9c3311f-7316-48d6-bf10-d810e70b4304
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b2091b4f19d5110e34c61ea7776214b740fc38f8
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919777"
---
# <a name="azure-data-lake-store-source"></a>Azure Data Lake Store 來源

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **Azure Data Lake Store 來源** 元件可讓 SSIS 套件從 Azure Data Lake Store 讀取資料。 支援的檔案格式：文字和 Avro。
  
 **Azure Data Lake Store 來源**是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。  
  
> [!NOTE]
> 為確保 Azure Data Lake Store 連線管理員及使用它的元件 (即 Azure Data Lake Store 來源及 Azure Data Lake Store 目的地) 能夠連接服務，請務必從 [這裡](https://www.microsoft.com/download/details.aspx?id=49492)下載最新版的 Azure Feature Pack。 
  
## <a name="configure-the-azure-data-lake-store-source"></a>設定 Azure Data Lake Store 來源
 1. 若要查看 Azure Data Lake Store 來源的編輯器，可在資料流程設計師上拖放 **Azure Data Lake Store 來源** ，並連按兩下以開啟編輯器。  
  
2.  在 [Azure Data Lake Store 連線管理員]  欄位指定現有的 Azure Data Lake Store 連線管理員，或建立參考 Azure Data Lake Store 服務的新連線管理員。  
  
    1.  在 [檔案路徑]  欄位指定 Azure Data Lake Store 來源檔案的檔案路徑。   
  
    2.  在 [檔案格式]  欄位指定來源檔案的檔案格式。  
  
        檔案格式若為文字，則您必須指定 [資料行分隔符號字元]  值。 若檔案中第一個資料列包含資料行名稱，請選取 [第一個資料列的資料行名稱]  。  
  
3.  指定連接資訊後，請切換至 [資料行]  頁面，將來源資料行對應至 SSIS 資料流程的目的地資料行。   

## <a name="text-qualifier"></a>文字定位項

**Azure Data Lake Store 來源**不支援文字限定詞。 若必須指定文字限定詞，才能正確處理您的檔案，請考慮將檔案下載到您的本機電腦，然後使用**一般檔案來源**處理這些檔案。 「一般檔案來源」可讓您指定文字限定詞。 如需詳細資訊，請參閱[ 一般檔案來源](flat-file-source.md)。
