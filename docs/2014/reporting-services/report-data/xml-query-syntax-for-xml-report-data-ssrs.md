---
title: XML 報表資料的 XML 查詢語法 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces [Reporting Services]
- data processing extensions [Reporting Services], data sources
- xmldp [Reporting Services]
- XML [Reporting Services], data retrieval
ms.assetid: d203886f-faa1-4a02-88f5-dd4c217181ef
caps.latest.revision: 46
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7697f6bf230b3d37b145e56f6827895b44daa5c0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37226998"
---
# <a name="xml-query-syntax-for-xml-report-data-ssrs"></a>XML 報表資料的 XML 查詢語法 (SSRS)
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，可以建立 XML 資料來源的資料集。 當您定義資料來源之後，要建立此資料集的查詢。 您可以根據資料來源所指向的 XML 資料類型，建立資料集查詢來包含 XML`Query`或元素路徑。 XML`Query`開頭**\<查詢 >** 標記，並且包含命名空間和資料來源而異的 XML 項目。 元素路徑與命名空間無關，而且會指定當搭配類似 XPath 語法使用基礎 XML 資料時，要使用哪些節點和節點屬性。 如需項目路徑的詳細資訊，請參閱 [XML 報表資料的項目路徑語法 &#40;SSRS&#41;](report-data-ssrs.md)。  
  
 您可以針對下列 XML 資料類型建立 XML 資料來源：  
  
-   使用 http 通訊協定由 URL 所指向的 Xml 文件  
  
-   傳回 XML 資料的 Web 服務端點  
  
-   內嵌 XML 資料  
  
 指定 XML `Query` 或元素路徑的方式會因 XML 資料類型而異。  
  
 是 XML 文件，XML`Query`是選擇性的。 如果它包含在內，它可以包含選擇性的 XML `ElementPath`， XML `ElementPath` 的值會使用元素路徑語法。 加入 XML`Query`和 XML`ElementPath`才能正確處理命名空間，它需要從資料來源的 XML 資料時。  
  
 如果是連接字串 URL 所指向的 Web 服務端點，XML `Query` 會定義此 Web 服務方法、SOAP 動作，或兩者皆定義。 XML 資料提供者會建立一個 Web 服務要求來擷取要用於報表的 XML 資料。  
  
> [!NOTE]  
>  當 Web 服務命名空間包含斜線 (`/)` 字元時，請同時加入 Web 服務方法和 SOAP 動作，好讓 XML 資料處理延伸模組可以正確衍生此命名空間。  
  
 是內嵌的 XML 文件，XML`Query`定義要使用的內嵌的 XML 資料，包括選擇性的命名空間，和包含選擇性 XML `ElementPath`...  
  
## <a name="specifying-query-parameters-for-xml-data"></a>指定 XML 資料的查詢參數  
 您可以指定 XML 文件的查詢參數。  
  
-   針對 URL 要求，查詢參數會包含為標準 URL 參數。  
  
-   針對 Web 服務要求，查詢參數會傳遞至 Web 服務方法。 若要定義查詢參數，請使用 [資料集屬性] 對話方塊的 [參數] 頁面。 如需詳細資訊，請參閱 <<c0> [ 資料集屬性對話方塊、 參數](dataset-properties-dialog-box-parameters.md)。  
  
### <a name="example"></a>範例  
 下表中的範例會說明如何從報表伺服器 Web 服務、XML 文件和內嵌 XML 資料中擷取資料。  
  
|XML 資料來源|查詢範例|  
|---------------------|-------------------|  
|ListChildren 方法從 web 服務 XML 資料。|`<Query>`<br /><br /> `<Method Name="ListChildren" Namespace="http://schemas.microsoft.com/sqlserver/2005/06/30/reporting/reportingservices" />`<br /><br /> `</Query>`|  
|SoapAction 中的 Web 服務 XML 資料。|`<Query xmlns=namespace>`<br /><br /> `<SoapAction>http://schemas/microsoft.com/sqlserver/2005/03/23/reporting/reportingservices/ListChildren</SoapAction>`<br /><br /> `</Query>`|  
|使用命名空間的 XML 文件或內嵌 XML 資料。<br /><br /> 指定元素路徑之命名空間的查詢元素。|`<Query xmlns:es="http://schemas.microsoft.com/StandardSchemas/ExtendedSales">`<br /><br /> `<ElementPath>/Customers/Customer/Orders/Order/es:LineItems/es:LineItem</ElementPath>`<br /><br /> `</Query>`|  
|內嵌 XML 文件。|`<Query>`<br /><br /> `<XmlData>`<br /><br /> `<Customers>`<br /><br /> `<Customer ID="1">Bobby</Customer>`<br /><br /> `</Customers>`<br /><br /> `</XmlData>`<br /><br /> `<ElementPath>Customer {@}</ElementPath>`<br /><br /> `</Query>`|  
|使用預設值的 XML 文件。|*沒有查詢*。<br /><br /> 元素路徑衍生自 XML 文件本身，而且與命名空間無關。|  
  
> [!NOTE]  
>  第一個 Web 服務範例會使用 <xref:ReportService2006.ReportingService2006.ListChildren%2A> 方法中的 Web 服務 XML 資料。 若要執行這個查詢，您必須建立新的資料來源，然後設定 http://localhost/reportserver/reportservice2006.asmx 的連接字串。 <xref:ReportService2006.ReportingService2006.ListChildren%2A>方法會採用兩個參數：`Item`和`Recursive`。 設定的預設值`Item`要`/`並`Recursive`至`1`。  
  
## <a name="specifying-namespaces"></a>指定命名空間  
 使用 XML`Query`項目來指定所使用的命名空間中的資料來源中的 XML 資料。 下列 XML 查詢會使用命名空間 `sales`。 `sales:LineItems` 和 `sales:LineItem` 的 XML `ElementPath` 節點會使用命名空間 `sales`。  
  
```  
<Query xmlns:sales=  
"http://schemas.microsoft.com/StandardSchemas/ExtendedSales">  
   <SoapAction>  
      http://schemas.microsoft.com/SalesWebService/ListOrders   
   </SoapAction>  
   <ElementPath>  
      Customers/Customer/Orders/Order/sales:LineItems/sales:LineItem  
   </ElementPath>  
</Query>  
```  
  
 若要指定資料提供者命名空間，以便預設命名空間留白，使用`xmldp`。 下列範例會顯示這一點。  
  
### <a name="example"></a>範例  
 下列範例會使用 XML 文件 DPNamespace.xml，這個文件是當做表格之後的說明； 這個表格會顯示包含命名空間前置詞的兩個 XML ElementPath 語法範例。  
  
|XML 查詢元素|在資料集中產生欄位|  
|-----------------------|-------------------------------------|  
|\<Query/>|值 a: http://schemas.microsoft.com/..<br /><br /> 值 b: http://schemas.microsoft.com/..<br /><br /> 值 c: http://schemas.microsoft.com/..|  
|\<xmldp:Query xmlns:xmldp ="http://schemas.microsoft.com/sqlserver/2005/02/reporting/XmlDPQuery"xmlns:ns ="http://schemas.microsoft.com/.. 」><br /><br /> \<xmldp:ElementPath > 根{}/ns:Element2 / 節點\</xmldp:ElementPath ><br /><br /> \</xmldp:Query >|D 值<br /><br /> E 值<br /><br /> F 值|  
  
#### <a name="xml-document-dpnamespacexml"></a>XML 文件：DPNamespace.xml  
 您可以複製這段 XML，並將它儲存為報表設計師可以使用的 URL，以便當做 XML 資料來源使用；例如 http://localhost/DPNamespace.xml。  
  
```  
<Root xmlns:ns="http://schemas.microsoft.com/...">  
   <ns:Element1>  
      <Node>Value A</Node>  
      <Node>Value B</Node>  
      <Node>Value C</Node>  
   </ns:Element1>  
   <ns:Element2>  
      <Node>Value D</Node>  
      <Node>Value E</Node>  
      <Node>Value F</Node>  
   </ns:Element2>  
</Root>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 連接類型 &#40;SSRS&#41;](xml-connection-type-ssrs.md)   
 [Reporting Services 教學課程 &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  
