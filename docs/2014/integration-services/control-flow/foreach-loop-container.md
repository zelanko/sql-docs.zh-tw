---
title: Foreach 迴圈容器 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.f1
helpviewer_keywords:
- repeating control flow
- Foreach Loop containers
- foreach enumerators [Integration Services]
- containers [Integration Services], Foreach Loop
ms.assetid: dd6cc2ba-631f-4adf-89dc-29ef449c6933
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d31e81b28ef28a60ac9d7bc44f81327bc0591db4
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433075"
---
# <a name="foreach-loop-container"></a>Foreach 迴圈容器
  「Foreach 迴圈」容器定義封裝中重複的控制流程。 迴圈實作與程式設計語言中 **Foreach** 迴圈的結構類似。 在封裝中，迴圈是使用 Foreach 列舉值啟用。  「Foreach 迴圈」容器會為指定列舉值的每個成員重複控制流程。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 提供下列列舉值類型：  
  
-   Foreach ADO 列舉值，用來列舉資料表中的資料列。 例如，您可以在 ADO 資料錄集中取得資料列。  
  
     資料錄集目的地會將記憶體中的資料儲存到 `Object` 資料類型之封裝變數中儲存的資料錄集。 您通常會使用具有 Foreach ADO 列舉值的 Foreach 迴圈容器來一次處理資料錄集的一個資料列。 針對 Foreach ADO 列舉值指定的變數必須屬於 Object 資料類型。 如需有關資料錄集目的地的詳細資訊，請參閱＜ [Use a Recordset Destination](../data-flow/recordset-destination.md)＞。  
  
-   「Foreach ADO.NET 結構描述資料列集」列舉值，用來列舉有關資料來源的結構描述資訊。 例如，您可以列舉並取得一份 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中資料表的清單。  
  
-   「Foreach 檔案」列舉值，用來列舉資料夾中的檔案。 列舉值可往返子資料夾。 例如，您可以讀取 Windows 資料夾及其子資料夾中所有副檔名為 *.log 的檔案。  
  
-   Foreach From Variable 列舉值，用來列舉指定的變數所包含的可列舉物件。 可列舉物件可以是陣列、ADO.NET `DataTable`、[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 列舉值等等。 例如，您可以列舉包含伺服器名稱之陣列的值。  
  
-   「Foreach 項目」列舉值，用來列舉集合項目。 例如，您可以列舉「執行處理」工作使用之可執行檔與工作目錄的名稱。  
  
-   Foreach Nodelist 列舉值，用來列舉 XML 路徑語言 (XPath) 運算式的結果集。 例如，此運算式會列舉並取得一份古典時期所有作者的清單： `/authors/author[@period='classical']`。  
  
-   Foreach SMO 列舉值，用來列舉 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) 物件。 例如，您可以列舉並取得一份 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中檢視的清單。  
  
-   Foreach Azure Blob 列舉值會列舉在 Azure 儲存體 blob 容器中的 Blob。  
  
-   Foreach ADLS 檔案列舉值，用來列舉 ADLS 目錄中的檔案。
  
 下列圖表顯示擁有「檔案系統」工作的「Foreach 迴圈」容器。 Foreach 迴圈會使用「Foreach 檔案」列舉值，而「檔案系統」工作則設定為複製檔案。 如果列舉值指定的資料夾含有四個檔案，則迴圈會重複四次並複製四個檔案。  
  
 ![列舉資料夾的 Foreach 迴圈容器](../media/ssis-foreachloop.gif "列舉資料夾的 Foreach 迴圈容器")  
  
 您可以使用變數和屬性運算式的組合，以列舉值集合值更新封裝物件的屬性。 首先，對應集合值與使用者定義的變數，接著在使用該變數的屬性上實作屬性運算式。 例如，「Foreach 檔案」列舉值的集合值會對應至名為的變數，然後在「傳送郵件」工作的 `MyFile` Subject 屬性的屬性運算式中使用該變數。 當執行封裝時，便會在每次迴圈重複時以某個檔案名稱更新 Subject 屬性。 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](../expressions/use-property-expressions-in-packages.md)。  
  
 對應至列舉值集合值的變數亦可在運算式和指令碼中使用。  
  
 「Foreach 迴圈」容器可包含多項工作和容器，但它只能使用一種列舉值。 如果「Foreach 迴圈」容器包含多項工作，您可將列舉值集合值對應至每項工作的多個屬性。  
  
 您可以在「Foreach 迴圈」容器上設定交易屬性，用來定義封裝控制流程子集的交易。 您可利用此方式於「Foreach 迴圈」層級管理交易，而非封裝層級。 例如，如果「Foreach 迴圈」容器重複更新星狀結構描述中維度和事實資料表的控制流程，則可設定交易以確認所有事實資料表均成功更新，或不更新任何資料表。 如需詳細資訊，請參閱 [Integration Services 交易](../integration-services-transactions.md)。  
  
## <a name="enumerator-types"></a>列舉值類型  
 列舉值可加以設定，而您必須根據列舉值提供不同的資訊。  
  
 下表摘要說明各列舉值類型所需的資訊。  
  
|列舉值|組態需求|  
|----------------|--------------------------------|  
|Foreach ADO|指定 ADO 物件來源變數和列舉值模式。 此變數必須屬於 Object 資料類型。|  
|Foreach ADO.NET 結構描述資料列集|指定資料庫的連接和要列舉的結構描述。|  
|Foreach 檔案|指定資料夾和要列舉的檔案、所擷取檔案的檔名格式，以及是否往返子資料夾。|  
|Foreach From Variable|指定包含要列舉物件的變數。|  
|Foreach 項目|定義「Foreach 項目」集合中的項目，包括資料行和資料行資料類型。|  
|Foreach Nodelist|指定 XML 文件的來源並設定 XPath 作業。|  
|Foreach SMO|指定資料庫的連接和要列舉的 SMO 物件。|  
|Foreach Azure Blob|指定包含要列舉之 blob 的 Azure blob 容器。|  
|Foreach ADLS 檔案|指定包含要列舉之檔案的 ADLS 目錄，以及一些篩選準則。|
  
## <a name="property-expressions-in-foreach-loop-containers"></a>Foreach 迴圈容器中的屬性運算式  
 封裝可以設定成同時執行多個可執行檔。 當封裝包含實作屬性運算式的「Foreach 迴圈」容器時，請謹慎使用這項組態。  
  
 實作屬性運算式通常非常適合用來設定「Foreach 迴圈」列舉值所使用之連線管理員的 ConnectionString 屬性值。 ConnectionString 的屬性運算式是由對應至列舉值之集合值的變數加以設定，並於迴圈的每個反覆運算中進行更新。  
  
 為了避免可執行檔平行執行時機不確定的負面影響，您應該將封裝設定為一次只執行一個可執行檔。 例如，如果封裝可以同時執行多項工作，當執行 SQL 工作的兩個執行個體試圖同時進行寫入時，負責列舉資料夾中的檔案、擷取檔案名稱，然後使用執行 SQL 工作將檔案名稱插入資料表等步驟的「Foreach 迴圈」容器可能會引發寫入衝突。 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](../expressions/use-property-expressions-in-packages.md)。  
  
## <a name="related-tasks"></a>相關工作  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關如何在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中設定這些屬性的詳細資訊，請按下列主題之一：  
  
-   [設定 Foreach 迴圈容器](foreach-loop-container.md)  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
 如需如何以程式設計方式設定這些屬性的詳細資訊，請按以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
## <a name="related-content"></a>相關內容  
 bidn.com 上的部落格文章： [SSIS ForEach NodeList 列舉值](https://go.microsoft.com/fwlink/?LinkId=220671)。  
  
## <a name="see-also"></a>另請參閱  
 [控制流程](control-flow.md)   
 [整合服務容器](integration-services-containers.md)  
  
  
