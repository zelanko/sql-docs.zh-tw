---
title: 關聯性 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb047cdd332861f6cfbff16dda6a536544369c1c
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2018
---
# <a name="relationships"></a>關聯性 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  在表格式模型中，關聯性是指兩個資料表之間的連接。 關聯性會建立兩個資料表中的資料相互關聯的方式。 例如，Customers 資料表和 Orders 資料表可以產生關聯，以便顯示彼此有關聯性的客戶名稱。  
  
 當使用 [資料表匯入精靈] 從相同資料來源匯入時，您選擇要匯入之資料表 (位於資料來源) 中已存在的關聯性會在模型中重新建立。 您可以使用 [圖表檢視] 中的模型設計師或使用 [管理關聯性] 對話方塊，檢視偵測到且自動重新建立的關聯性。 您也可以使用 [圖表檢視] 中的模型設計師或使用 [建立關聯性] 或 [管理關聯性] 對話方塊，手動建立資料表之間的新關聯性。  
  
 在定義兩個資料表之間的關聯性 (無論是匯入期間自動建立或手動建立) 之後，便能夠使用相關資料行篩選資料以及在相關資料表中查閱值。  
  
> [!TIP]  
>  如果您的模型包含許多關聯性，[圖表檢視] 可協助您更妥善地視覺化及建立資料表之間的新關聯性。  
  
  
##  <a name="what"></a> 優點  
 關聯性是在兩個資料表之間，以每個資料表中的一個或多個資料行為基礎的連接。 若要了解為什麼關聯性是有用的，請假設您在追蹤自己商務中的客戶訂單資料。 您可以在具有類似下列結構的單一資料表中追蹤所有資料：  
  
|CustomerID|名稱|EMail|DiscountRate|OrderID|OrderDate|產品|Quantity|  
|----------------|----------|-----------|------------------|-------------|---------------|-------------|--------------|  
|1|Ashton|chris.ashton@contoso.com|.05|256|2010-01-07|Compact Digital|11|  
|1|Ashton|chris.ashton@contoso.com|.05|255|2010-01-03|SLR Camera|15|  
|2|Jaworski|michal.jaworski@contoso.com|.10|254|2010-01-03|Budget Movie-Maker|27|  
  
 這種方法可能有效，但牽涉到儲存太多重複的資料，例如每筆訂單的客戶電子郵件地址。 儲存雖然廉價，但是如果電子郵件地址變更，您就需要確定更新該客戶的每個資料列。 此問題的一種解決方案，就是將資料分為多個資料表，並且定義這些資料表之間的關聯性。 這是中使用的方法*關聯式資料庫*像 SQL Server。 例如，您匯入模型的資料庫可能會使用三個相關的資料表來表示訂單資料：  
  
### <a name="customers"></a>客戶  
  
|[CustomerID]|名稱|EMail|  
|--------------------|----------|-----------|  
|1|Ashton|chris.ashton@contoso.com|  
|2|Jaworski|michal.jaworski@contoso.com|  
  
### <a name="customerdiscounts"></a>CustomerDiscounts  
  
|[CustomerID]|DiscountRate|  
|--------------------|------------------|  
|1|.05|  
|2|.10|  
  
### <a name="orders"></a>Orders  
  
|[CustomerID]|OrderID|OrderDate|產品|Quantity|  
|--------------------|-------------|---------------|-------------|--------------|  
|1|256|2010-01-07|Compact Digital|11|  
|1|255|2010-01-03|SLR Camera|15|  
|2|254|2010-01-03|Budget Movie-Maker|27|  
  
 如果從相同資料庫匯入這些資料表，[資料表匯入精靈] 即可根據 [方括號] 中的資料行來偵測資料表之間的關聯性，而且可以在模型設計師中重現這些關聯性。 如需詳細資訊，請參閱本主題中的 [關聯性的自動偵測和推斷](#detection) 。 如果您從多個來源匯入資料表，您可以手動建立關聯性中所述[建立資料表之間的關聯兩個](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)。  
  
### <a name="columns-and-keys"></a>資料行與索引鍵  
 關聯性是以包含相同資料的每個資料表中的資料行為基礎。 例如，「客戶」和「訂單」資料表可以彼此相關，因為兩者都包含儲存客戶 ID 的資料行。 在此範例中，資料行名稱相同，但這點並不是需求。 一個資料行可以是 CustomerID，另一個資料行則可是 CustomerNumber，只要「訂單」資料表中所有包含 ID 的資料列也都有儲存在「客戶」資料表中即可。  
  
 在關聯式資料庫中，有幾種類型的 *「索引鍵」*(Key)，這些通常只是具有特殊屬性的資料行。 在關聯式資料庫中，可以使用下列四種類型的索引鍵：  
  
-   「主索引鍵」：可以唯一識別資料表中的資料列，例如 Customers 資料表中的 CustomerID。  
  
-   「其他索引鍵」(又稱「候選索引鍵」)：不同於主索引鍵的唯一資料行。 例如，「員工」資料表可能儲存員工 ID 和社會保險號碼，兩者都是唯一的。  
  
-   「外部索引鍵」：參考另一個資料表中唯一資料行的資料行，例如 Orders 資料表中的 CustomerID，這指的是 Customers 資料表中的 CustomerID。  
  
-   *「複合索引鍵」*(Composite Key)：由一個以上資料行所組成的索引鍵。 表格式模型不支援複合索引鍵。 如需詳細資訊，請參閱本主題中的＜複合索引鍵與查閱資料行＞。  
  
 在表格式模型中，主索引鍵或替代索引鍵稱為 *「相關查閱資料行」*(Related lookup column)，或簡稱 *「查閱資料行」*(Lookup column)。 如果資料表同時具有主索引鍵和替代索引鍵，您就可以使用其中任一種做為查閱資料行。 外部索引鍵又稱為 *「來源資料行」* (Source Column) 或簡稱 *「資料行」*(Column)。 在我們的範例中，會在「訂單」資料表中的 CustomerID (資料行) 與「客戶」資料表中的 CustomerID (查閱資料行) 之間定義關聯性。 如果從關聯式資料庫匯入資料，模型設計師就會依預設從一個資料表選擇外部索引鍵，並從另一個資料表選擇對應的主索引鍵。 不過，您可以使用在查閱資料行具有唯一值的任何資料行。  
  
### <a name="types-of-relationships"></a>關聯性的類型  
 Customers 和 Orders 之間的關聯性是「一對多關聯性」。 每個客戶可以有許多張訂單，但是每張訂單不能有多個客戶。 其他類型的關聯性則是「一對一」和「多對多」。 定義每個客戶之單一折扣率的 CustomerDiscounts 資料表，與「客戶」資料表之間就具有一對一的關聯性。 Products 與 Customers 之間的直接關聯性就是多對多關聯性的範例，其中客戶可以購買許多產品，而且相同的產品可以由許多客戶購買。 模型設計師的使用者介面不支援多對多關聯性。 如需詳細資訊，請參閱本主題中的＜[多對多關聯性](#bkmk_many_to_many)＞。  
  
 下表顯示三個資料表之間的關聯性：  
  
|關聯性|型別|「查閱資料行」|「資料行」|  
|------------------|----------|-------------------|------------|  
|Customers-CustomerDiscounts|一對一|Customers.CustomerID|CustomerDiscounts.CustomerID|  
|Customers-Orders|一對多|Customers.CustomerID|Orders.CustomerID|  
  
### <a name="relationships-and-performance"></a>關聯性與效能  
 建立任何關聯性之後，模型設計師通常都必須重新計算使用新建立關聯性中資料表之資料行的任何公式。 視資料量與關聯性的複雜度而定，可能需要一些時間進行處理。  
  
##  <a name="requirements"></a> Requirements for relationships  
 模型設計師在建立關聯性時，具有多項必須遵循的需求：  
  
### <a name="single-active-relationship-between-tables"></a>資料表之間的單一使用中關聯性  
 多個關聯性可能會在資料表之間造成模稜兩可的相依性。 若要建立精確的計算，您需要從一個資料表到下一個資料表的單一路徑。 因此，每一對資料表之間只能有一個使用中的關聯性。 例如，在 AdventureWorks DW 2012 中，資料表 DimDate 包含一個資料行 DateKey，這個資料行與資料表 FactInternetSales 中的三個不同資料行相關：OrderDate、DueDate 與 ShipDate。 如果您嘗試匯入這些資料表，會成功建立第一個關聯性，但是對於包含相同資料行的後續關聯性，則會收到下列錯誤：  
  
 \* 關聯性： 資料表 [column 1]-> table [column 2]-狀態： 錯誤-原因： 無法建立資料表之間的關聯性\<資料表 1 > 和\<表格 2 >。 兩個資料表之間只能有一個直接或間接關聯性。  
  
 如果您有兩個資料表，而且在這兩個資料表之間有多個關聯性，則您需要匯入包含查閱資料行之資料表的多個複本，然後在每對資料表之間建立一個關聯性。  
  
 資料表之間可以有許多非使用中的關聯性。 資料表之間要使用的路徑是在查詢時由報表用戶端指定。  
  
### <a name="one-relationship-for-each-source-column"></a>每個來源資料行一個關聯性  
 來源資料行無法參與多個關聯性。 如果您已經使用一個資料行做為某個關聯性中的來源資料行，但是想要使用該資料行連接至不同資料表中的其他相關查閱資料行，您可以建立資料行的複本，然後將該資料行用於新的關聯性。  
  
 建立具有完全相同之值的資料行複本相當容易，只要在導出資料行中使用 DAX 公式即可。 如需詳細資訊，請參閱[建立導出資料行](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md)。  
  
### <a name="unique-identifier-for-each-table"></a>每個資料表的唯一識別碼  
 每個資料表都必須具有能夠唯一識別該資料表中每個資料列的單一資料行。 此資料行通常稱為主索引鍵。  
  
### <a name="unique-lookup-columns"></a>唯一查閱資料行  
 查閱資料行中的資料值必須是唯一的。 換句話說，資料行不能包含重複的值。 在表格式模型中，雖然空值和空白字串相當於空白，卻是不同的資料值。 這表示您無法在查閱資料行中有多個 Null 值。  
  
### <a name="compatible-data-types"></a>相容的資料類型  
 來源資料行和查閱資料行中的資料類型都必須相容。 如需資料類型的詳細資訊，請參閱[支援的資料類型](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md)。  
  
### <a name="composite-keys-and-lookup-columns"></a>複合索引鍵和查閱資料行  
 您無法在表格式模型中使用複合索引鍵；您必須永遠具備一個可唯一識別資料表中每個資料列的資料行。 若您嘗試匯入含有以複合索引鍵為基礎之現有關聯性的資料表，[資料表匯入精靈] 將會忽略該關聯性，因為它無法在表格式模型中建立。  
  
 若您想在模型設計師中建立兩個資料表之間的關聯性，但其中有多個資料行定義主索引鍵及外部索引鍵，您就必須在建立關聯性之前，先合併這些值以建立單一索引鍵資料行。 您可以在匯入資料之前執行這項作業，也可以在模型設計師中透過建立導出資料行來執行。  
  
###  <a name="bkmk_many_to_many"></a> Many-to-Many relationships  
 表格式模型不支援多對多關聯性，而且您無法直接在模型設計師中加入 *「聯合資料表」* (Junction table)。 不過，您可以使用 DAX 函數來塑造多對多關聯性。  
  
 您也可以嘗試設定雙向交叉篩選，以查看它是否可達到相同目的。 有時多對多關聯性的需求可以透過滿足，交叉篩選保存跨多個資料表關聯性的篩選內容。 如需詳細資訊，請參閱 [SQL Server 2016 Analysis Services 中適用於表格式模型的雙向交叉篩選](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) 。  
  
### <a name="self-joins-and-loops"></a>自我聯結與迴圈  
 在表格式模型資料表中不允許使用自我聯結。 自我聯結是資料表和本身之間的遞迴關聯性。 自我聯結通常用來定義父子式階層。 例如，您可以將 Employees 資料表聯結到其本身，以產生會顯示商務中管理鏈結的階層。  
  
 模型設計師不允許在模型的關聯性之間建立迴圈。 換句話說，系統禁止下列這組關聯性。  
  
 資料表 1 的資料行 a - 資料表 2 的資料行 f  
  
 資料表 2 的資料行 f - 資料表 3 的資料行 n  
  
 資料表 3 的資料行 n - 資料表 1 的資料行 a  
  
 如果您嘗試建立的關聯性會建立迴圈，則會產生錯誤。  
  
##  <a name="detection"></a> Inference of relationships  
 在某些情況下，資料表之間的關聯性會自動鏈結。 例如，如果您在以下前兩組資料表之間建立關聯性，就會推斷另外兩個資料表之間也有關聯性，然後自動建立關聯性。  
  
 產品和類別 -- 手動建立  
  
 產品和子類別 -- 手動建立  
  
 產品和子類別 -- 推斷出關聯性  
  
 為了讓關聯性能夠自動鏈結，如上所示，關聯性都必走向同一個方向。 如果初始的關聯性是在「銷售」和「產品」，以及「銷售」和「客戶」之間，就不會推斷出關聯性。 這是因為「產品」和「客戶」之間的關聯性是多對多關聯性。  
  
##  <a name="bkmk_detection"></a> Detection of relationships when importing data  
 當您從關聯式資料來源資料表匯入時，資料表匯入精靈會根據來源結構描述資料來偵測這些來源資料表內的現有關聯性。 如果匯入相關資料表，將會在模型中複製這些關聯性。  
  
##  <a name="bkmk_manually_create"></a> Manually create relationships  
 雖然單一關聯式資料來源中資料表之間的大多數關聯性都會被自動偵測到並在表格式模型中建立，但在許多情況下必須手動建立模型資料表之間的關聯性。  
  
 如果您的模型包含來自多個資料來源的資料，則可能需要手動建立關聯性。 例如，您可以從關聯式資料來源匯入 Customers、CustomerDiscounts 和 Orders 資料表。 來源中這些資料表之間的現有關聯式會在模型中自動建立。 然後，您可以從不同來源新增其他資料表，例如，從 Microsoft Excel 活頁簿中的 Geography 資料表匯入地區資料。 接著手動建立 Customers 資料表中的資料行和 Geography 資料表中的資料行之間的關聯性。  
  
 若要在表格式模型中手動建立關聯性，您可以使用 [圖表檢視] 中的模型設計師或使用 [管理關聯性] 對話方塊。 此圖表檢視以圖形格式顯示資料表，以及資料表之間的關聯性。 您可以按一下一個資料表中的資料行，將游標拖曳到另一個資料表中，輕鬆地在兩個資料表之間以正確順序建立關聯性。 [管理關聯性] 對話方塊以簡單的表格格式顯示資料表之間的關聯性。 若要了解如何手動建立關聯性，請參閱[建立資料表之間的關聯兩個](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)。  
  
##  <a name="bkmk_dupl_errors"></a> Duplicate values and other errors  
 如果您選擇不能用於關聯性的資料行，資料行旁邊就會出現紅色的 X。 您可以將游標暫停在錯誤圖示上方，以檢視訊息，其中提供有關此問題的詳細資訊。 以下列出的問題，可能會使得所選資料行之間無法建立關聯性：  
  
|問題或訊息|解決方案|  
|------------------------|----------------|  
|由於所選取的兩個資料行包含重複值，無法建立關聯性。|若要建立有效的關聯性，您所選取的一對中至少有一個資料行必須只包含唯一值。<br /><br /> 您可以編輯資料行以移除重複項目，也可以反轉資料行的順序，以便使用包含唯一值的資料行做為 **[相關查閱資料行]**。|  
|資料行包含 Null 值或空白值。|資料行無法以 Null 值，彼此進行聯結。 針對每個資料列，在兩個資料行中都必須有在關聯性中用到的值。|  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|主題|Description|  
|-----------|-----------------|  
|[建立兩個資料表之間的關聯性](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)|描述如何手動建立兩個資料表之間的關聯性。|  
|[刪除關聯性](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)|描述如何刪除關聯性和刪除關聯性的後果。|  
|[SQL Server 2016 Analysis Services 中適用於表格式模型的雙向交叉篩選](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)|描述相關資料表的雙向交叉篩選。 如果資料表相關聯，並且定義雙向交叉篩選，則在跨第二個資料表關聯性進行查詢時，可以使用一個資料表關聯性的篩選內容。|  
  
## <a name="see-also"></a>另請參閱  
 [資料表和資料行](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [匯入資料](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)  
  
  
