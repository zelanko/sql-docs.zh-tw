---
title: 第 1 課：使用 SSIS 來建立專案和基本套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 84d0b877-603f-4f8e-bb6b-671558ade5c2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ff31579a425f9e86fed11811c9d0a42c3113ee15
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79288132"
---
# <a name="lesson-1-create-a-project-and-basic-package-with-ssis"></a>第 1 課：使用 SSIS 來建立專案和基本套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在本課程中，您將建立一個簡單的 ETL 套件，此套件會從單一一般檔案來源擷取資料、使用兩個查閱轉換來轉換資料，然後將轉換的資料寫入至 **AdventureWorksDW2012** 範例資料庫中 **FactCurrencyRate** 事實資料表的複本。 在本課程中，您會了解如何建立新套件、新增和設定資料來源與目的地連線，以及使用新的控制流程和資料流程元件。  
  
在建立套件之前，您必須先了解來源資料和目的地中使用的格式。 接著，您便可以定義將來源資料與目的地對應所需的轉換。  

## <a name="prerequisites"></a>Prerequisites

本教學課程倚賴 Microsoft SQL Server Data Tools，這是一組範例套件及一個範例資料庫。

* 若要安裝 SQL Server Data Tools，請參閱[下載 SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md)。  
  
* 下載本教學課程的所有課程套件：

    1.  瀏覽至 [Integration Services 教學課程檔案](https://www.microsoft.com/download/details.aspx?id=56827) \(英文\)。

    2.  選取 [Download] \(下載\)  按鈕。

    3.  選取 [Creating a Simple ETL Package.zip] \(建立簡單的 ETL Package.zip\)  檔案，然後選取 [Next] \(下一步\)  。

    4.  下載檔案之後，將其內容解壓縮至本機目錄。  

* 若要安裝並部署 **AdventureWorksDW2012** 範例資料庫，請參閱[安裝及設定 AdventureWorks 範例資料庫 - SQL](../samples/adventureworks-install-configure.md)。
  
## <a name="look-at-the-source-data"></a>查看資料來源
在本教學課程中，來源資料是名為 **SampleCurrencyData.txt** 之一般檔案中的一組歷史貨幣資料。 來源資料具有下列四個資料行：貨幣的平均匯率、貨幣索引鍵、日期索引鍵和收盤匯率。  
  
以下是 SampleCurrencyData.txt 檔案中的來源資料範例：  
  
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
  
使用一般檔案來源資料時，請務必了解「一般檔案」連線管理員如何解譯一般檔案資料。 如果一般檔案來源是 Unicode，一般檔案連接管理員會將所有資料行定義為 [DT_WSTR]，預設資料行寬度為 50。 如果一般檔案來源是以 ANSI 編碼，資料行就會定義為 [DT_STR]，且預設資料行寬度為 50。 您可能必須變更這些預設值，以便讓字串資料行類型更適用於您的資料。 您必須查看目的地的資料類型，然後在「一般檔案」連線管理員內選擇該類型。  
  
## <a name="look-at-the-destination-data"></a>查看目的地資料
來源資料的目的地是 **AdventureWorksDW** 中 **FactCurrencyRate** 事實資料表的複本。 **FactCurrencyRate** 事實資料表有四個資料行，且與兩個維度資料表之間有關聯性，如下表所示。  
  
|資料行名稱|資料類型|查閱資料表|「查閱資料行」|  
|---------------|-------------|----------------|-----------------|  
|AverageRate|FLOAT|None|None|  
|CurrencyKey|int (FK)|DimCurrency|CurrencyKey (PK)|  
|DateKey|int (FK)|DimDate|DateKey (PK)|  
|EndOfDayRate|FLOAT|None|None|  
  
## <a name="map-the-source-data-to-the-destination"></a>將來源資料對應至目的地  
我們的來源和目的地資料格式分析指出查閱對 **CurrencyKey** 和 **DateKey** 值而言是必要的。 執行這些查閱的轉換會使用來自**DimCurrency** 和 **DimDate** 維度資料表的替代索引鍵來取得這些值。  
  
|一般檔案資料行|資料表名稱|資料行名稱|資料類型|  
|--------------------|--------------|---------------|-------------|  
|0|FactCurrencyRate|AverageRate|FLOAT|  
|1|DimCurrency|CurrencyAlternateKey|nchar(3)|  
|2|DimDate|FullDateAlternateKey|date|  
|3|FactCurrencyRate|EndOfDayRate|FLOAT|  
  
## <a name="lesson-tasks"></a>課程工作  
這一課包含下列工作：  
  
-   [步驟 1：建立新的 Integration Services 專案](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
-   [步驟 2：新增及設定一般檔案連線管理員](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
-   [步驟 3：新增及設定 OLE DB 連線管理員](../integration-services/lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
-   [步驟 4：將資料流程工作新增至套件](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
-   [步驟 5：新增及設定一般檔案來源](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
-   [步驟 6：新增及設定查閱轉換](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
-   [步驟 7：新增及設定 OLE DB 目的地](../integration-services/lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
-   [步驟 8：為第 1 課套件加上註解並設定格式](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
-   [步驟 9：測試第 1 課套件](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>開始課程  
[步驟 1：建立新的 Integration Services 專案](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
