---
title: 課程 1：使用 SSIS 建立專案和基本套件 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 84d0b877-603f-4f8e-bb6b-671558ade5c2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a4431e593a74c7f6a656f78cd70abfd19c813bdd
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51642075"
---
# <a name="lesson-1-create-a-project-and-basic-package-with-ssis"></a>第 1 課：使用 SSIS 建立專案和基本套件

在這一課，您將建立一個從單個一般檔案來源擷取資料的簡易 ETL 套件，使用兩個查閱轉換元件來轉換資料、將該資料寫入至 **AdventureWorksDW2012** 中的 **FactCurrencyRate** 事實資料表複本。 在這一課，您會學到如何建立新封裝，加入和設定資料來源和目的地連接，以及使用新控制流程和資料流程元件。  
  
> [!IMPORTANT]  
> 這個教學課程需要 **AdventureWorksDW2012** 範例資料庫。 如需有關安裝和部署 **AdventureWorksDW2012**的資訊，請參閱 [CodePlex 上的 Reporting Services 產品範例](https://go.microsoft.com/fwlink/p/?LinkID=526910)。  
  
## <a name="understanding-the-package-requirements"></a>了解封裝需求  
這個教學課程需要 Microsoft SQL Server Data Tools。  
  
如需安裝 SQL Server Data Tools 的詳細資訊，請參閱 [SQL Server Data Tools 下載](https://msdn.microsoft.com/data/hh297027)。  
  
在建立封裝之前，您需要了解來源資料和目的地使用的格式。 了解這些資料格式之後，您就可以定義必要的轉換，將來源資料對應至目的地。  
  
### <a name="looking-at-the-source"></a>查看來源  
在這個教學課程中，來源資料是一般檔案 SampleCurrencyData.txt 中所含的貨幣記錄資料集。 來源資料具有下列四個資料行：貨幣的平均匯率、貨幣索引鍵、日期索引鍵和收盤匯率。  
  
以下是包含在 SampleCurrencyData.txt 檔案中的來源資料範例：  
  
<pre>1.00070049USD9/3/05 0:001.001201442  
1.00020004USD9/4/05 0:001  
1.00020004USD9/5/05 0:001.001201442  
1.00020004USD9/6/05 0:001  
1.00020004USD9/7/05 0:001.00070049  
1.00070049USD9/8/05 0:000.99980004  
1.00070049USD9/9/05 0:001.001502253  
1.00070049USD9/10/05 0:000.99990001  
1.00020004USD9/11/05 0:001.001101211  
1.00020004USD9/12/05 0:000.99970009</pre>  
  
使用一般檔案來源資料時，一定要了解一般檔案連接管理員如何解譯一般檔案資料。 如果一般檔案來源是 Unicode，一般檔案連接管理員會將所有資料行定義為 [DT_WSTR]，預設資料行寬度為 50。 如果一般檔案來源是以 ANSI 編碼，資料行會定義為 [DT_STR]，且資料行寬度為 50。 您或許必須變更這些預設值，好讓字串資料行類型更適合您的資料。 若要這麼做，您必須查看要在其中寫入資料的目的地之資料類型，然後在一般檔案連接管理員內選擇正確類型。  
  
### <a name="looking-at-the-destination"></a>查看目的地  
來源資料的最終目的地是 **AdventureWorksDW** 中的 **FactCurrencyRate** 事實資料表複本。 **FactCurrencyRate** 事實資料表有四個資料行，且與兩個維度資料表之間有關聯性，如下表所示。  
  
|資料行名稱|資料類型|查閱資料表|查閱資料行|  
|---------------|-------------|----------------|-----------------|  
|AverageRate|FLOAT|None|None|  
|CurrencyKey|int (FK)|DimCurrency|CurrencyKey (PK)|  
|DateKey|int (FK)|DimDate|DateKey (PK)|  
|EndOfDayRate|FLOAT|None|None|  
  
### <a name="mapping-source-data-to-be-compatible-with-the-destination"></a>對應來源資料以便與目的地相容  
來源和目的地資料格式的分析指出 **CurrencyKey** 和 **DateKey** 值可能需要查閱。 要執行這些查閱的轉換將使用 **DimCurrency** 和 **DimDate** 維度資料表的替代索引鍵來取得 **CurrencyKey** 和 **DateKey** 值。  
  
|一般檔案資料行|資料表名稱|資料行名稱|資料類型|  
|--------------------|--------------|---------------|-------------|  
|0|FactCurrencyRate|AverageRate|float|  
|1|DimCurrency|CurrencyAlternateKey|nchar(3)|  
|2|DimDate|FullDateAlternateKey|日期|  
|3|FactCurrencyRate|EndOfDayRate|FLOAT|  
  
## <a name="lesson-tasks"></a>課程工作  
這一課包含下列工作：  
  
-   [步驟 1：建立新的 Integration Services 專案](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
-   [步驟 2：新增和設定一般檔案連線管理員](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
-   [步驟 3：新增和設定 OLE DB 連線管理員](../integration-services/lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
-   [步驟 4：將資料流程工作新增至套件中](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
-   [步驟 5：新增和設定一般檔案來源](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
-   [步驟 6：新增及設定查閱轉換](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
-   [步驟 7：新增及設定 OLE DB 目的地](../integration-services/lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
-   [步驟 8：使第 1 課的套件更容易了解](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
-   [步驟 9：測試第 1 課的教學課程封裝](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>開始課程  
[步驟 1：建立新的 Integration Services 專案](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
