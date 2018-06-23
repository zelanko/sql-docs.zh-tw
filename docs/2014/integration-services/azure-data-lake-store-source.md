---
title: Azure Data Lake Store 來源 | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSSRC.F1
- SQL11.DTS.DESIGNER.AFPADLSSRC.F1
ms.assetid: 7d9e8457-62aa-4aea-98ee-7d1121dfae4f
caps.latest.revision: 6
author: yualan
ms.author: yual
manager: jhubbard
ms.openlocfilehash: e7bd327dc2657123daf94390785bda11a17e2040
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029858"
---
# <a name="azure-data-lake-store-source"></a>Azure Data Lake Store 來源
  **Azure Data Lake Store 來源** 元件可讓 SSIS 套件從 Azure Data Lake Store 讀取資料。 支援的檔案格式為文字和 Avro。
  
## <a name="configure-the-azure-data-lake-store-source"></a>設定 Azure Data Lake Store 來源 
  
1.  若要查看 Azure Data Lake Store 來源的編輯器，可在資料流程設計師上拖放 **Azure Data Lake Store 來源** ，並連按兩下以開啟編輯器。  
  
2.  在 [Azure Data Lake Store 連線管理員]  欄位指定現有的 Azure Data Lake Store 連線管理員，或建立參考 Azure Data Lake Store 服務的新連線管理員。  
  
    1.  在 [檔案路徑]  欄位指定 Azure Data Lake Store 來源檔案的檔案路徑。   
  
    2.  在 [檔案格式]  欄位指定來源檔案的檔案格式。  
  
        檔案格式若為文字，則您必須指定 [資料行分隔符號字元]  值。 若檔案中第一個資料列包含資料行名稱，請選取 [第一個資料列的資料行名稱]  。  
  
3.  指定連接資訊後，請切換至 [資料行]  頁面，將來源資料行對應至 SSIS 資料流程的目的地資料行。  