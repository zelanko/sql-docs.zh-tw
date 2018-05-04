---
title: XML 資料類型和資料行 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 00db8f21-7d4b-4347-ae43-3a7c314d2fa1
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4fa1ea2ba7eb9742d4596a1ce403a42038d2d842
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="xml-data-type-and-columns-sql-server"></a>XML 資料類型和資料行 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  本主題討論 **中** xml [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型的優勢和限制，並幫助您選擇儲存 XML 資料的方式。  
  
## <a name="relational-or-xml-data-model"></a>關聯式或 XML 資料模型  
 如果您的資料使用已知的結構描述來高度結構化，則關聯式模型對資料儲存來說可能是最好的方式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供必要的功能以及您可能需要的工具。 另一方面，如果結構是半結構化或是無結構，或是情況不明，您就必須考慮將這類資料模型化。  
  
 如果您想要一個與平台沒有關聯的模型，以使用結構化及語意化的標記來確保資料的可攜性，則 XML 會是個很好的選擇。 此外，若符合下列的部份屬性，XML 也會是很適當的選項：  
  
-   您的資料很少，或是您不知道資料的結構，或是資料的結構未來可能會有重大變更。  
  
-   您的資料代表內含項目階層，而不是實體之間的參考，而且可能是遞迴式的。  
  
-   順序是資料固有的。  
  
-   您想要依據資料結構來查詢資料，或是更新部份資料。  
  
 若沒有符合上述任一情況，則您應使用關聯式資料模型。 例如，若資料為 XML 格式，但您的應用程式只是使用資料庫來儲存及擷取資料，您就只需要 **[n]varchar(max)** 資料行。 將資料儲存在 XML 資料行中還有其他好處， 其中包括可由引擎來判斷資料結構是否良好以及資料是否有效，也包括了細部查詢及 XML 資料更新的支援。  
  
## <a name="reasons-for-storing-xml-data-in-sql-server"></a>將 XML 資料儲存在 SQL Server 中的理由  
 以下是一些在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用原生 XML 功能，而不在檔案系統中管理 XML 資料的理由：  
  
-   您想要以有效率及交易性的方式來共用、查詢及修改 XML 資料。 細項資料存取權對您的應用程式很重要。 例如，您想要在 XML 文件中擷取某幾段，或是您想要插入新的區段，而不要置換整份文件。  
  
-   您有關聯式資料及 XML 資料，而且您希望應用程式中的關聯式及 XML 資料之間具有互通性。  
  
-   您需要語言支援，以進行跨網域應用程式的查詢及資料修改。  
  
-   您希望伺服器能保證資料的結構良好，並依據 XML 結構描述來選擇驗證您的資料。  
  
-   您想要檢索 XML 資料，以求查詢處理的效率及良好的可調適性，並使用第一級的查詢最佳化工具。  
  
-   您想要有 XML 資料的 SOAP、ADO.NET 及 OLE DB 存取權。  
  
-   您想要利用資料庫伺服器的管理功能來管理您的 XML 資料。 例如，您想要備份、復原及複寫資料。  
  
 如果沒有符合上述任一情況，可能比較適合將您的資料儲存成非 XML 的大型物件類型，例如 **[n]varchar(max)** 或 **varbinary(max)**。  
  
## <a name="xml-storage-options"></a>XML 儲存選項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 XML 儲存選項如下：  
  
-   原生儲存為 **xml** 資料類型  
  
     以內部表示法來儲存資料，以保存資料的 XML 內容。 這個內部表示法包括有關內含項目階層、文件順序，以及元素和屬性值的資訊。 特別是會保存 XML 資料的 InfoSet 內容。 如需 InfoSet 的詳細資訊，請前往 [http://www.w3.org/TR/xml-infoset](http://go.microsoft.com/fwlink/?LinkId=48843)。 InfoSet 內容可能會與文字版 XML 不同，因為沒有保留下列資訊：不重要的空格、屬性的順序、命名空間前置詞及 XML 宣告。  
  
     針對具類型的 **xml** 資料類型 (與 XML 結構描述繫結的 **xml** 資料類型)，後置結構描述驗證 InfoSet (PSVI) 會將類型資訊加入 InfoSet 中，而且會以內部表示法來編碼。 這樣可以大幅增加剖析的速度。 如需詳細資訊，請參閱 [http://www.w3.org/TR/xmlschema-1](http://go.microsoft.com/fwlink/?LinkId=48881) 和 [http://www.w3.org/TR/xmlschema-2](http://go.microsoft.com/fwlink/?LinkId=4871) 的「W3C XML 結構描述」規格。  
  
-   XML 與關聯式儲存之間的對應  
  
     藉由使用註解式結構描述 (AXSD)，XML 會被分解成一或多個資料表中的資料行。 如此可以讓資料的精確度保持在關聯式層級。 這樣一來，雖然會忽略元素之間的順序，但會保留階層結構。 結構描述不能遞迴。  
  
-   大型的物件儲存體 **[n]varchar(max)** 和 **varbinary(max)**  
  
     會儲存相同的資料副本。 針對特殊目的應用程式 (如：法律文件)，這是很有用的。 大部份的應用程式都不需要完全相同的副本，且可以滿足於 XML 內容 (InfoSet 精確度)。  
  
 一般而言，您可能必須組合使用這些方法。 例如，您想要將 XML 資料儲存在 **xml** 資料類型資料行中，並將其屬性升級為關聯式資料行。 或者，您想要使用對應技術來將非遞迴的部分儲存在非 XML 資料行中，並只將遞迴的部分儲存在 **xml** 資料類型資料行中。  
  
### <a name="choice-of-xml-technology"></a>XML 技術的選項  
 XML 技術的選項有原生 XML 和 XML 檢視，通常需視下列因素而定：  
  
-   儲存選項  
  
     您的 XML 資料可能比較適合大型物件儲存體 (例如，產品手冊)，或是比較適合儲存在關聯式資料行中 (例如，轉換成 XML 的線性項目)。 每個儲存選項保留的文件精確度各不相同。  
  
-   查詢功能  
  
     根據查詢的本質，以及您查詢 XML 資料的程度，您可能會發現其中一個儲存選項比另一個更合適。 在這兩種儲存選項中，支援 XML 資料細項查詢 (例如：XML 節點的述詞評估) 的程度各不相同。  
  
-   檢索 XML 資料  
  
     您可能會想要檢索 XML 資料，以加速 XML 查詢的效能。 索引選項會依儲存選項而有所不同；您必須做出適當的選擇，以使您的工作負載最佳化。  
  
-   資料修改功能  
  
     有些工作負載需要修改 XML 資料的細項。 例如，可能需要在文件中加入新的區段，但在其他工作負載中 (例如：Web 內容) 則不需要。 對您的應用程式而言，資料修改的語言支援可能是很重要的。  
  
-   結構描述支援  
  
     您用來描述 XML 資料的結構描述可能是也可能不是 XML 結構描述文件。 與結構描述繫結之 XML 的支援取決於 XML 技術。  
  
 不同的選擇也會有不同的效能特質。  
  
### <a name="native-xml-storage"></a>原生 XML 儲存  
 您可以將 XML 資料儲存在伺服器的 **xml** 資料類型資料行中。 若符合下列情況，則適用此選項：  
  
-   您想要直接將 XML 資料儲存在伺服器，同時也要保持文件順序和文件結構。  
  
-   您可能有也可能沒有 XML 資料的結構描述。  
  
-   您想要查詢及修改 XML 資料。  
  
-   您想要檢索 XML 資料，以加速查詢處理。  
  
-   您的應用程式需要系統目錄檢視來管理 XML 資料及 XML 結構描述。  
  
 當您的 XML 文件有一個結構範圍，或是您的 XML 文件符合相異或複雜的結構描述，而這些結構描述難以對應到關聯式結構時，原生 XML 儲存是很有用的。  
  
#### <a name="example-modeling-xml-data-using-the-xml-data-type"></a>範例：使用 xml 資料類型來將 XML 資料模型化  
 假設有一個 XML 格式的產品手冊，其中每個主題各成一章，每一章中有好幾節。 每一節中還可包含小節。 因此，\<section> 就是遞迴項目。 產品手冊包含大量的混合內容、圖表和技術資料；資料是半結構化的。 使用者可能會想要在內容中搜尋感興趣的主題，例如，在有關「檢索」的那一章中搜尋有關「叢集索引」的那一節，並查詢技術數量。  
  
 您的 XML 文件所適合的儲存模式就是 **xml** 資料類型資料行。 這樣可以保持 XML 資料的 InfoSet 內容。 檢索 XML 資料行對於查詢效能是很有益的。  
  
#### <a name="example-retaining-exact-copies-of-xml-data"></a>範例：保留與 XML 資料完全相同的副本  
 舉例來說，假設政府規定您要保留與您的 XML 文件完全相同的原文副本。 例如，這些可能是簽署的文件、法律文件或股票交易訂單。 您可能會想要將您的文件儲存在 **[n]varchar(max)** 資料行中。  
  
 若要查詢，請在執行階段將資料轉換成 **xml** 資料類型，並對其執行 Xquery。 執行階段的轉換作業可能會很耗費資源，尤其是當文件很大時。 若您經常查詢，您可以另外將文件儲存在 **xml** 資料類型資料行中，當您從 **[n]varchar(max)** 資料行傳回完全相同的文件副本時，再加以檢索。  
  
 XML 資料行可能是以 **[n]varchar(max)** 資料行為基礎的計算資料行。 但是您不能在計算的 XML 資料行上建立 XML 索引，也不能在 **[n]varchar(max)** 或 **varbinary(max)** 資料行上建立 XML 索引。  
  
### <a name="xml-view-technology"></a>XML 檢視技術  
 在您的 XML 結構描述與資料庫中的資料表之間定義對應，即可建立永續性資料的「XML 檢視」。 藉由 XML 檢視，可使用 XML 大量載入功能來擴展基礎資料表。 您可以使用 XPath 1.0 版來查詢 XML 檢視；該查詢會在資料表上轉換成 SQL 查詢。 同樣地，更新內容也會傳播至那些資料表。  
  
 在下列狀況下，這項技術非常有用：  
  
-   您想要有一個以 XML 為中心的程式設計模型，透過現有的關聯式資料來使用 XML 檢視。  
  
-   您有一個用於 XML 資料的結構描述 (XSD、XDR)，是由外部協力廠商提供的。  
  
-   在您的資料中，順序並不重要，或者您的查詢資料表資料不是遞迴式的，或者事先已知道可達到的最大遞迴深度。  
  
-   您想要使用 XPath 1.0 透過 XML 檢視來查詢及修改資料。  
  
-   您想要使用 XML 檢視來大量載入 XML 資料，並將其分解在基礎資料表中。  
  
 範例包括在資料交換及 Web 服務中公開為 XML 的關聯式資料，以及含有固定結構描述的 XML 資料。 如需詳細資訊，請參閱 [MSDN Online Library](http://go.microsoft.com/fwlink/?linkid=31174)。  
  
#### <a name="example-modeling-data-using-an-annotated-xml-schema-axsd"></a>範例：使用註解式 XML 結構描述 (AXSD) 來將資料模型化  
 舉例來說，假設您要將現有的關聯式資料 (例如：客戶、訂單及線性項目) 處理成 XML。 在關聯式資料上使用 AXSD，以定義 XML 檢視。 XML 檢視可讓您將 XML 資料大量載入至資料表中，並使用 XML 檢視來查詢及更新關聯式資料。 如果您必須在不干擾 SQL 應用程式工作的情況下，與其他應用程式交換含有 XML 標記的資料，這種模型會很有用。  
  
### <a name="hybrid-model"></a>混合模型  
 關聯式與 **xml** 資料類型資料行的組合最常適用於資料的模型化。 XML 資料中有些值可以儲存在關聯式資料行中，其餘的值 (或是整個 XML 值) 則可儲存在 XML 資料行中。 這樣可能會產生較佳的效能，因為對於以關聯式資料行及鎖定特性來建立的索引，您會有比較大的控制權。  
  
 至於要將哪些值儲存在關聯式資料行中，則需視您的工作負載而定。 例如，若您是依據路徑運算式 /Customer/@CustId 來擷取所有的 XML 值，則將 **CustId** 屬性值升級至關聯式資料行中並加以檢索，可能會產生較快的查詢效能。 另一方面，如果 XML 資料是廣泛且毫不多餘地分解在關聯式資料行中，則重組的成本可能會很大。  
  
 例如，針對高度結構化的 XML 資料，資料表的內容都已轉換成 XML；您可以將所有值對應到關聯式資料行，可能還會用到 XML 檢視技術。  
  
## <a name="granularity-of-xml-data"></a>XML 資料的資料粒度  
 儲存在 XML 資料行中之 XML 資料的資料粒度對於鎖定動作是很重要的，姑且不論這一點，它對於更新也是很重要的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 針對 XML 和非 XML 資料都是使用相同的鎖定機制。 因此，資料列層級的鎖定會導致資料列中所有的 XML 執行個體被鎖定。 若資料粒度大，則鎖定大型 XML 執行個體來進行更新時，將會導致在多使用者情況下的輸送量降低。 另一方面，嚴重的分解也會失去物件封裝，並增加重組成本。  
  
 在滿足資料模型化需求與鎖定和更新特性之間取得平衡，對於良好的設計是很重要的。 然而，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，實際儲存的 XML 執行個體大小就沒那麼重要了。  
  
 例如，對 XML 執行個體進行更新時，是使用對部份二進位大型物件 (BLOB) 和部份索引更新的新支援，其中會將目前已儲存的 XML 執行個體與其更新版本做比較。 部份二進位大型物件 (BLOB) 更新作業會在這二個 XML 執行個體之間執行差異比較，並且只更新差異的部份。 部分索引更新作業只會修改那些必須在 XML 索引中變更的資料列。  
  
## <a name="limitations-of-the-xml-data-type"></a>xml 資料類型的限制  
 請注意下列適用於 **xml** 資料類型的一般限制：  
  
-   **xml** 資料類型執行個體的預存表示法不能超過 2 GB。  
  
-   它無法當作 **sql_variant** 執行個體的子類型使用。  
  
-   它不支援轉換 (Cast 或 Convert) 為 **text** 或 **ntext**。 改用 **varchar(max)** 或 **nvarchar(max)** 。  
  
-   它無法加以比較或排序。 這表示 **xml** 資料類型無法用在 GROUP BY 陳述式中。  
  
-   它無法當作 ISNULL、COALESCE 和 DATALENGTH 以外之任何純量、內建函數的參數。  
  
-   它無法當作索引中的索引鍵資料行使用。 但是，在建立非叢集索引時使用 INCLUDE 關鍵字，可以將它包含在叢集索引中做為資料，或明確地將它加入非叢集索引中。  
  
## <a name="see-also"></a>另請參閱  
 [大量匯入與匯出 XML 文件的範例 &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
