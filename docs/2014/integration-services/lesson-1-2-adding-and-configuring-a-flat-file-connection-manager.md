---
title: 步驟 2：新增和設定一般檔案連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 9a77dd32-d8c2-4961-ad37-2a971f9d6043
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e2d22c652ce63bfc3069756251ff554a5d13c186
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197348"
---
# <a name="step-2-adding-and-configuring-a-flat-file-connection-manager"></a>步驟 2：加入和設定一般檔案連接管理員
  在這項工作中，您將一般檔案連接管理員加入您剛才建立的封裝中。 一般檔案連接管理員可讓封裝從一般檔案擷取資料。 使用一般檔案連接管理員，您可以指定當封裝從一般檔案擷取資料時，要套用的檔案名稱和位置、地區設定和字碼頁及檔案格式 (包括資料行分隔符號)。 此外，您可以手動指定個別資料行的資料類型，或使用 [建議資料行類型] 對話方塊，將所擷取資料的資料行自動對應至 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 資料類型。  
  
 您必須為您要使用的每一個檔案格式建立新的一般檔案連接管理員。 因為這個教學課程是從多個具有相同資料格式的一般檔案擷取資料，所以您只需要在封裝中加入和設定一個一般檔案連接管理員。  
  
 在此教學課程中，您將在一般檔案連接管理員中設定下列屬性：  
  
-   **資料行名稱** ：因為一般檔案沒有資料行名稱，所以一般檔案連接管理員會建立預設資料行名稱。 這些預設名稱無助於識別每一個資料行所代表的內容。 若要使這些預設名稱有所幫助，您必須將預設名稱變更為符合一般檔案資料即將載入的事實資料表的名稱。  
  
-   **資料對應**：所有參考連接管理員的一般檔案資料來源元件，將使用您為一般檔案連接管理員指定的資料類型對應。 您可以使用一般檔案連接管理員來手動對應資料類型，或使用 [建議資料行類型] 對話方塊。 在此教學課程中，您將檢視在 [建議資料行類型] 對話方塊中建議的對應，然後在 [一般檔案連接管理員編輯器] 對話方塊中手動做一些必要的對應。  
  
 一般檔案連接管理員提供有關資料檔的地區設定資訊。 如果電腦未設定為使用 [英文 (美國)] 地區選項，則您必須在 [一般檔案連接管理員編輯器] 對話方塊中設定其他屬性。  
  
### <a name="to-add-a-flat-file-connection-manager-to-the-ssis-package"></a>若要將一般檔案連接管理員加入至 SSIS 封裝  
  
1.  以滑鼠右鍵按一下 [連接管理員] 區域的任何位置，然後按一下 [新增一般檔案連接]。  
  
2.  在 [一般檔案連接管理員編輯器] 對話方塊中，對 [連接管理員名稱] 輸入 [範例一般檔案來源資料]。  
  
3.  按一下 **[瀏覽]**。  
  
4.  在 [開啟] 對話方塊中，尋找電腦上的 SampleCurrencyData.txt 檔案。  
  
     範例資料隨附在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 課程封裝中。 若要下載範例資料和課程封裝，請執行下列動作。  
  
    1.  導覽至 [Integration Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  按一下 **[下載]** 索引標籤。  
  
    3.  按一下 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 檔案。  
  
5.  清除第一個資料列核取方塊中的資料行名稱。  
  
### <a name="to-set-locale-sensitive-properties"></a>若要設定區分地區設定屬性  
  
1.  在 [一般檔案連接管理員編輯器] 對話方塊中，按一下 [一般]。  
  
2.  將 [地區設定] 設為 [英文 (美國)]，將 [字碼頁] 設為 1252。  
  
### <a name="to-rename-columns-in-the-flat-file-connection-manager"></a>若要重新命名一般檔案連接管理員中的資料行  
  
1.  在 [一般檔案連接管理員編輯器] 對話方塊中，按一下 [進階]。  
  
2.  在屬性窗格中，進行下列變更：  
  
    -   變更**Column 0、column** name 屬性來`AverageRate`。  
  
    -   變更**資料行 1** name 屬性來`CurrencyID`。  
  
    -   變更**資料行 2** name 屬性來`CurrencyDate`。  
  
    -   變更**資料行 3** name 屬性來`EndOfDayRate`。  
  
    > [!NOTE]  
    >  依預設，所有 4 個資料行一開始是設為字串資料類型 [DT_STR]，且 `OutputColumnWidth` 為 50。  
  
### <a name="to-remap-column-data-types"></a>若要重新對應資料行資料類型  
  
1.  在 [一般檔案連接管理員編輯器] 對話方塊中，按一下 [建議類型]。  
  
     [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會依據最前面的 200 個資料列，自動建議最適合的資料類型。 您也可以變更這些建議選項，以增加或減少取樣資料、指定整數或布林資料的預設資料類型，或是加入空格以填補字串資料行。  
  
     目前請暫時不要對 [建議資料行類型] 對話方塊中的選項做任何變更，並按一下 [確定]，由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 建議適合資料行的資料類型。 這時會回到 [一般檔案連接管理員編輯器] 對話方塊的 [進階] 窗格，您可以在此檢視 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 建議的資料行資料類型。 (如果按一下 [取消]，則不會對資料行中繼資料做出任何建議，而是使用預設的字串 (DT_STR) 資料類型)。  
  
     在這個教學課程中，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會對 SampleCurrencyData.txt 檔案的資料建議下列資料表中第二個資料行所顯示的資料類型。 不過，目的地的資料行所需要的資料類型 (將在後面的步驟中定義) 將顯示在下表的最後一個資料行。  
  
    |一般檔案資料行|建議類型|目的地資料行|目的地類型|  
    |----------------------|--------------------|------------------------|----------------------|  
    |AverageRate|float [DT_R4]|FactCurrency.AverageRate|FLOAT|  
    |CurrencyID|string [DT_STR]|DimCurrency.CurrencyAlternateKey|nchar(3)|  
    |CurrencyDate|date [DT_DATE]|DimDate.FullDateAlternateKey|日期|  
    |EndOfDayRate|float [DT_R4]|FactCurrency.EndOfDayRate|FLOAT|  
  
     適用於資料類型建議`CurrencyID`資料行是與目的地資料表中的欄位的資料類型不相容。 因為資料類型`DimCurrency.CurrencyAlternateKey`是 nchar (3)，`CurrencyID`必須從字串 [DT_STR] 字串變更為 [DT_WSTR]]。 此外，欄位`DimDate.FullDateAlternateKey`定義為日期資料類型; 因此，`CurrencyDate`需要從日期 [DT_Date] 變更為資料庫日期 [DT_DBDATE]。  
  
2.  在清單中，選取 [currencyid] 資料行，然後在 [屬性] 窗格中，變更 [資料行的資料類型`CurrencyID`，從 Unicode 字串 [DT_STR] 字串 [DT_WSTR]。  
  
3.  在 [屬性] 窗格中，變更 [資料行的資料型別`CurrencyDate`從日期 [DT_DATE] 為資料庫日期 [DT_DBDATE]。  
  
4.  按一下 [確定] 。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 3：新增和設定 OLE DB 連線管理員](lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
## <a name="see-also"></a>另請參閱  
 [一般檔案連接管理員](connection-manager/file-connection-manager.md)   
 [Integration Services 資料類型](data-flow/integration-services-data-types.md)  
  
  
