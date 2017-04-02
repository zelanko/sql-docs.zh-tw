---
title: "步驟 6：加入及設定查閱轉換 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 5c59f723-9707-4407-80ae-f05f483cf65f
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# 步驟 6：加入及設定查閱轉換
在設定一般檔案來源從來源檔擷取資料之後，下一項工作是要定義所需要的查閱轉換來取得 **CurrencyKey** 和 **DateKey** 的值。 查閱轉換是藉由聯結指定輸入資料行中的資料與參考資料集內的資料行來執行查閱。 參考資料集可以是現有的資料表或檢視、新資料表，或 SQL 陳述式的結果。 在此教學課程中，查閱轉換使用 OLE DB 連接管理員來連接到資料庫，該資料庫包含的資料就是參考資料集的來源。  
  
> [!NOTE]  
> 您也可以將查閱轉換設定為連接到包含參考資料集的快取。 如需相關資訊，請參閱 [Lookup Transformation](../integration-services/data-flow/transformations/lookup-transformation.md)。  
  
在此教學課程中，您會在封裝中加入和設定下列兩個查閱轉換元件：  
  
-   一個轉換是基於一般檔案中相符的 **CurrencyID** 資料行值，來查閱 **DimCurrency** 維度資料表之 **CurrencyKey** 資料行的值。  
  
-   一個轉換是基於一般檔案中相符的 **CurrencyDate** 資料行值，來查閱 **DimDate** 維度資料表之 **DateKey** 資料行的值。  
  
在這兩種案例中，查閱轉換將利用您先前建立的 OLE DB 連接管理員。  
  
### 若要加入及設定查閱貨幣索引鍵轉換  
  
1.  在 [SSIS 工具箱] 中，展開 [通用]，然後將 [查閱] 拖曳至 [資料流程] 索引標籤的設計介面中。 將 [查閱] 直接放在 [擷取範例貨幣資料] 來源下面。  
  
2.  按一下 [擷取範例貨幣資料] 一般檔案來源，將綠色箭頭拖曳至新加入的 [查閱] 轉換來連接兩個元件。  
  
3.  在 [資料流程] 設計介面中，按一下 [查閱] 轉換中的 [查閱]，將名稱變更為**查閱貨幣索引鍵**。  
  
4.  按兩下 [查閱貨幣索引鍵] 轉換，即可顯示查閱轉換編輯器。  
  
5.  在 [一般] 頁面上，進行下列選擇：  
  
    1.  選取 [完整快取]。  
  
    2.  在 **[連接類型]** 區域中，選取 **[OLE DB 連接管理員]**。  
  
6.  在 [連接] 頁面上，進行下列選擇：  
  
    1.  在 [OLE DB 連線管理員] 對話方塊中，確定 [localhost.AdventureWorksDW2012] 已顯示。  
  
    2.  選取 [使用 SQL 查詢的結果]，然後輸入或複製下列 SQL 陳述式：  
  
        ```  
        select * from (select * from [dbo].[DimCurrency]) as refTable  
        where [refTable].[CurrencyAlternateKey] = 'ARS'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'AUD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'BRL'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'CAD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'CNY'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'DEM'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'EUR'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'FRF'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'GBP'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'JPY'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'MXN'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'SAR'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'USD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'VEB'  
        ```  
  
7.  在 [資料行] 頁面上，進行下列選擇：  
  
    1.  在 [可用的輸入資料行] 畫面中，將 [CurrencyID] 拖曳至 [可用的查閱資料行] 面板，並將它放在 [CurrencyAlternateKey] 中。  
  
    2.  在 [可用的查閱資料行] 清單中，選取 [CurrencyKey] 左邊的核取方塊。  
  
8.  按一下 [確定]，回到 [資料流程] 設計介面。  
  
9. 以滑鼠右鍵按一下 [查閱貨幣索引鍵] 轉換，然後按一下 [屬性]。  
  
10. 在 [屬性] 視窗中，確認 [LocaleID] 屬性是設為 [英文 (美國)]，[DefaultCodePage] 屬性是設為 [1252]。  
  
### 若要加入和設定查閱日期索引鍵轉換  
  
1.  在 [SSIS 工具箱] 中，將 [查閱] 拖曳至 [資料流程] 設計介面中。 將 [查閱] 直接放在 [查閱貨幣索引鍵] 轉換下面。  
  
2.  按一下 [查閱貨幣索引鍵] 轉換，將綠色箭頭拖曳至新加入的 [查閱] 轉換來連接兩個元件。  
  
3.  在 [輸入輸出選擇] 對話方塊的 [輸出] 清單方塊中，按一下 [查閱比對輸出]，然後按一下 [確定]。  
  
4.  在 [資料流程] 設計介面中，於新加入的 [查閱] 轉換中按一下 [查閱]，將名稱變更為**查閱日期索引鍵**。  
  
5.  按兩下 [查閱日期索引鍵] 轉換。  
  
6.  在 [一般] 頁面上，選取 [部分快取]。  
  
7.  在 [連接] 頁面上，進行下列選擇：  
  
    1.  在 [OLE DB 連線管理員] 對話方塊中，確定 [localhost.AdventureWorksDW2012] 已顯示。  
  
    2.  在 [使用資料表或檢視] 方塊中，輸入或選取 **[dbo].[DimDate]**。  
  
8.  在 [資料行] 頁面上，進行下列選擇：  
  
    1.  在 [可用的輸入資料行] 畫面中，將 [CurrencyDate] 拖曳至 [可用的查閱資料行] 面板，並將它放在 [FullDateAlternateKey] 中。  
  
    2.  在 [可用的查閱資料行] 清單中，選取 [DateKey] 左邊的核取方塊。  
  
9. 在 [進階] 頁面上，檢閱快取選項。  
  
10. 按一下 [確定]，回到 [資料流程] 設計介面。  
  
11. 以滑鼠右鍵按一下 [查閱日期索引鍵] 轉換，然後按一下 [屬性]。  
  
12. 在 [屬性] 視窗中，確認 [LocaleID] 屬性是設為 [英文 (美國)]，[DefaultCodePage] 屬性是設為 [1252]。  
  
## 本課程的下一項工作  
[步驟 7：加入及設定 OLE DB 目的地](../integration-services/step-7-adding-and-configuring-the-ole-db-destination.md)  
  
## 另請參閱  
[查閱轉換](../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
  
