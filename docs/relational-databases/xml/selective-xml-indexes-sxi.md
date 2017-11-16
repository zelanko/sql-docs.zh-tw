---
title: "選擇性 XML 索引 (SXI) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 598ecdcd-084b-4032-81b2-eed6ae9f5d44
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d0918df220f63cefec2319eb6d6585522b2e3fd4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="selective-xml-indexes-sxi"></a>選擇性 XML 索引 (SXI)
  選擇性 XML 索引是除了一般 XML 索引之外，另一種可供您使用 XML 索引類型。 選擇性 XML 索引功能的目標如下：  
  
-   改善 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中所儲存 XML 資料的查詢效能。  
  
-   支援更快索引大型 XML 資料工作負載。  
  
-   透過減少 XML 索引的儲存成本提升可調適性。  
  
 一般 XML 索引的主要限制在於會索引整份 XML 文件。 這樣會導致幾項重大錯誤，例如，查詢效能降低與索引維護成本增加，這些大部分與索引的儲存成本相關。  
  
 選擇性 XML 索引功能可讓您僅從 XML 文件升級要索引的特定路徑。 在建立索引時，這些路徑會經過評估，而這些路徑指向的節點會經過切割，並且儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的關聯式資料表內。 此功能使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Research 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產品小組共同開發的高效率對應演算法。 此演算法會將 XML 節點對應到單一關聯式資料表並達到絕佳的效能，同時只需要適度的儲存空間。  
  
 選擇性 XML 索引功能也支援在已由選擇性 XML 索引進行索引之節點上的次要選擇性 XML 索引。 這些次要選擇性索引不但有效率，還能進一步提升查詢效能。  
  
##  <a name="benefits"></a> 選擇性 XML 索引的優點  
 選擇性 XML 索引提供下列優點：  
  
1.  大幅提升對一般查詢負載之 XML 資料類型的查詢效能。  
  
2.  與一般 XML 索引相較之下，儲存需求更低。  
  
3.  與一般 XML 索引相較之下，索引維護成本減少。  
  
4.  不需要更新應用程式就能受益於選擇性 XML 索引的優點。  
  
  
##  <a name="compare"></a> 選擇性 XML 索引和主要 XML 索引  
  
> [!IMPORTANT]  
>  在大部分情況下，建立選擇性 XML 索引會比一般 XML 索引獲得更佳的效能和更有效率的儲存。  
  
 但是，下列任一情況為 true 時，不建議使用選擇性 XML 索引：  
  
-   對應大量節點路徑。  
  
-   在文件結構中支援未知元素或未知位置中元素的查詢。  
  
  
##  <a name="example"></a> 簡單的選擇性 XML 索引範例  
 在大約有 500,000 個資料列的資料表中將下列 XML 片段視為 XML 文件：  
  
```xml  
<book>  
    <created>2004-03-01</created>   
    <authors>Various</authors>  
    <subjects>  
        <subject>English wit and humor -- Periodicals</subject>  
        <subject>AP</subject>   
    </subjects>  
    <title>Punch, or the London Charivari, Volume 156, April 2, 1919</title>  
    <id>etext11617</id>  
</book>  
```  
  
 在這個簡單的結構描述中那麼多個資料列上建立主要 XML 索引，需要花很長的時間。 查詢此資料也會因為主要 XML 索引不支援選擇性索引而受到影響。  
  
 如果您只需要在 `/book/title` 路徑和 `/book/subjects` 路徑上查詢此資料，可以建立下列選擇性 XML 索引：  
  
```tsql  
CREATE SELECTIVE XML INDEX SXI_index  
ON Tbl(xmlcol)  
FOR   
(  
    pathTitle = '/book/title/text()' AS XQUERY 'xs:string',   
    pathAuthors = '/book/authors' AS XQUERY 'node()',  
    pathId = '/book/id' AS SQL NVARCHAR(100)  
)  
```  
  
 上述陳述式是 CREATE 語法的很好範例，您可在建立選擇性 XML 索引時使用。 在 CREATE 陳述式中，首先提供索引的名稱，並且識別要索引的資料表和 XML 資料行。 然後提供要索引的路徑。 路徑有三個部分：  
  
1.  可唯一識別路徑的名稱。  
  
2.  描述路徑的 XQuery 運算式。  
  
3.  選用的最佳化提示。  
  
 如需有關這些元素的詳細資訊，請參閱 [相關工作](#reltasks)。  
  
  
## <a name="supported-features-prerequisites-and-limitations"></a>支援的功能、必要條件和限制  
  
###  <a name="features"></a> 支援的 XML 功能  
 選擇性 XML 索引在 exist()、value() 和 nodes() 方法內支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所支援的 XQuery。  
  
-   對於 exist()、value() 和 nodes() 方法，選擇性 XML 索引包含足夠的資訊可轉換整個運算式。  
  
-   對於 query() 和 modify() 方法，選擇性 XML 索引可能只用於節點篩選。  
  
-   對於 query() 方法，選擇性 XML 索引不會用來擷取結果。  
  
-   對於 modify() 方法，選擇性 XML 索引不會用來更新 XML 文件。  
  
  
###  <a name="unsupported"></a> 不支援的 XML 功能  
 選擇性 XML 索引不支援 XML 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 實作中支援的下列功能：  
  
-   索引包含複雜 XS 類型的節點：聯集類型、序列類型和清單類型。  
  
-   索引包含二進位 XS 類型的節點：例如 base64Binary 和 hexBinary。  
  
-   使用結尾包含萬用字元 `*` 的 XPath 運算式指定要索引的節點：例如  `/a/b/c/*`、 `/a//b/*`或 `/a/b/*:c`。  
  
-   索引子系、屬性或下階以外的任何座標軸。 `//<step>` 案例可做為特殊案例。  
  
-   索引 XML 處理指示和註解。  
  
-   使用 id() 函數指定及擷取節點識別碼。  
  
  
###  <a name="prereq"></a> 必要條件  
 下列必要條件必須存在，您才能在使用者資料表中的 XML 資料行上建立選擇性 XML 索引：  
  
-   叢集索引必須存在於使用者資料表的主索引鍵上。  
  
-   搭配選擇性 XML 索引使用時，使用者資料表的主索引鍵大小限制為 128 個位元組。  
  
-   搭配選擇性 XML 索引使用時，使用者資料表的叢集索引鍵限制為 15 個資料行。  
  
  
###  <a name="limits"></a> 限制  
 **一般需求與限制**  
  
-   每一個選擇性 XML 索引只能在單一 XML 資料行上建立。  
  
-   您無法在非 XML 資料行上建立選擇性 XML 索引。  
  
-   資料表中的每個 XML 資料行只能包含一個選擇性 XML 索引。  
  
-   每一個資料表最多可以有 249 個選擇性 XML 索引。  
  
 **所支援物件的限制**  
  
 您無法在下列物件上建立選擇性 XML 索引：  
  
1.  檢視中的 XML 資料行。  
  
2.  XML 資料行的資料表值變數。  
  
3.  XML 類型變數。  
  
4.  計算 XML 資料行。  
  
5.  深度超過 128 個巢狀節點的 XML 資料行。  
  
 **有關儲存的限制**  
  
 對於 XML 文件中可加入至索引的節點數目會有某一限度的限制。 選擇性 XML 索引會將 XML 文件對應到單一關聯式資料表。 因此，它不能在資料表的任一資料列中擁有超過 1024 個非 null 資料行。 此外，疏鬆資料行的許多限制也會套用至選擇性 XML 索引，因為索引會使用疏鬆資料行進行儲存。  
  
 任一資料列中支援的非 null 資料行數目上限取決於資料行中資料的大小：  
  
-   在最好的情況下，如果所有資料行都是 **bit**類型，則可支援 1024 個非 null 資料行。  
  
-   在最差的情況下，如果所有資料行都是 **varchar**類型的大型物件，則只能支援 236 個非 null 資料行。  
  
 選擇性 XML 索引會在內部針對每一個索引的節點路徑使用一到四個資料行。 依據索引路徑中實際的資料大小而定，可進行索引的節點總數範圍可從 60 個到數百個節點。  
  
-   在最差的情況下，如果節點路徑定義中的部分或全部節點是使用 `//` 對應，則索引節點的最大數目為 60。  
  
-   在最好的情況下，如果節點路徑定義中的節點都不是使用 `//` 對應，則索引節點的最大數目為 200。  
  
 **選擇性 XML 索引會在您 CREATE 或 ALTER 索引時重建。**  
  
 當您 CREATE 或 ALTER 選擇性 XML 索引時，它會在單一執行緒的離線模式中重建。 太多 ALTER 陳述式會對索引之 XML 文件上的查詢效能產生負面影響。  
  
 **其他限制**  
  
-   查詢提示中不支援選擇性 XML 索引。  
  
-   Database Tuning Advisor 中不支援選擇性 XML 索引和次要選擇性 XML 索引。  
  
  
##  <a name="reltasks"></a> 相關工作  
  
|||  
|-|-|  
|**工作**|**主題**|  
|當您建立或修改選擇性 XML 索引時，指定您要建立索引的節點路徑，以及選用的最佳化提示。|[指定選擇性 XML 索引的路徑和最佳化提示](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)|  
|建立、修改或卸除選擇性 XML 索引。|[建立、修改和卸除選擇性 XML 索引](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)|  
|建立、修改或卸除次要選擇性 XML 索引。|[建立、修改和卸除次要選擇性 XML 索引](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)|  
  
  
  
