---
title: 報表定義語言 | Microsoft Docs
description: 了解報表定義語言 (RDL) 的相關詳細資料。 您將了解 RDL 是 SQL Server Reporting Services 報表定義的 XML 表示法。
ms.date: 01/24/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Reporting Services, RDL
- Reporting Services, RDL
- RDL [Reporting Services], about Report Definition Language
- SSRS, RDL
- Report Definition Language, about Report Definition Language
- Report Definition Language
- RDL [Reporting Services]
- reports [Reporting Services], definitions
ms.assetid: b18b025e-f4bd-4744-8f86-0ac9fb967548
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 04c220383ef14fe6bd05b690e5c27ae73b4289a4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "79510079"
---
# <a name="report-definition-language-ssrs"></a>報表定義語言 (SSRS)
  報表定義語言 (RDL) 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表定義的 XML 表示法。 報表定義包含報表的資料擷取和配置資訊。 RDL 是由符合針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]所建立之 XML 文法的 XML 元素所組成。 您可以加入自訂函數，藉由存取報表定義檔案中的程式碼組件來控制報表項目值、樣式和格式。  
  
 RDL 會藉由定義可啟用報表定義交換的常用結構描述來提升商業報表產品的互通性。 適用於 XML 的任何通訊協定或程式設計介面都可以搭配 RDL 使用。 RDL 是：  
  
-   報表定義的 XML 結構描述。  
  
-   企業與協力廠商的交換格式。  
  
-   可支援其他命名空間和自訂元素的可延伸與開放結構描述。  
  
##  <a name="rdl-specifications"></a><a name="bkmk_RDL_Specifications"></a> RDL 規格  
 若要下載特定結構描述版本的規格，請參閱 [Report Definition Language Specification](https://go.microsoft.com/fwlink/?linkid=116865)(報表定義語言規格)。  
  
##  <a name="rdl-xml-schema-definition"></a><a name="bkmk_RDL_XML_Schema_Definition"></a> RDL XML 結構描述定義  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表定義語言 (RDL) 檔案是藉由使用 XML 結構描述定義 (XSD) 檔案來驗證。 結構描述定義 RDL 元素可在 .rdl 檔案中何處發生的規則。 元素包括其資料類型和基數，也就是所允許的發生數目。 元素可能很簡單或很複雜。 簡單的元素沒有子元素或屬性 (Attribute)， 複雜的元素則具有子元素或屬性。  
  
 例如，此結構描述包含 RDL 元素 **ReportParameters**，這是複雜類型 **ReportParametersType**。 依照慣例，元素的複雜類型是在元素名稱後面加上 **Type**這個字。 **ReportParameters** 元素可由 **報表** 元素 (複雜類型) 所包含，而且可以包含 **ReportParameter** 元素。 **ReportParameterType** 是簡單類型，只能是下列其中一個值：**Boolean**、**DateTime**、**Integer**、**Float** 或 **String**。 如需 XML 結構描述資料類型的詳細資訊，請參閱 [XML Schema Part 2:Datatypes Second Edition](https://go.microsoft.com/fwlink/?linkid=4871) (XML 結構描述第 2 部分：資料類型第二版)。  
  
 RDL XSD 是在 ReportDefinition.xsd 檔案中提供的，這個檔案位於產品 CD-ROM 的 Extras 資料夾中， 也會透過下列 URL 提供在報表伺服器：`https://servername/reportserver/reportdefinition.xsd`。  
  
##  <a name="creating-rdl"></a><a name="bkmk_Creating_RDL"></a> 建立 RDL  
 因為 RDL 具有可延伸與開放的特質，所以可以建立各種工具和應用程式來根據其 XML 結構描述產生 RDL。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供用於建立 RDL 檔案的多個工具。 如需詳細資訊，請參閱 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)。  
  
 從應用程式產生 RDL 的一個最簡單方法，就是使用 <xref:System.Xml> 命名空間及 <xref:System.Linq> 命名空間的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 類別。 尤其是有一個類別 (亦即 **XmlTextWriter** 類別) 可用來撰寫 RDL。 有了 **XmlTextWriter**，您便可以在任何 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 應用程式中從頭到尾產生完整的報表定義。 開發人員也可以擴充 RDL，其方式是加入具有自訂屬性的自訂報表項目。 如需 **XmlTextWriter** 類別和 <xref:System.Xml> 命名空間的詳細資訊，請參閱《[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 開發人員指南》。 如需有關 Language-Integrated Query (LINQ) 的詳細資訊，請在 MSDN 上搜尋 "LINQ to XML"。  
  
 報表定義檔案的標準副檔名是 .rdl。 您也可以開發用戶端報表定義檔案，其副檔名為 .rdlc。 這兩種副檔名的 MIME 類型為 text/xml。 如需報表的詳細資訊，請參閱 [Reporting Services 報表 &#40;SSRS&#41;](../../reporting-services/reports/reporting-services-reports-ssrs.md)。  
  
##  <a name="rdl-types"></a><a name="bkmk_RDL_Types"></a> RDL 類型  
 下表列出用於 RDL 元素及屬性的類型。  
  
|類型|描述|  
|----------|-----------------|  
|**二進位**|具有 Base-64 編碼二進位值的屬性。|  
|**布林值**|具有 **true** 或 **false** 物件值的屬性。 除非另有指定，否則省略的選擇性布林物件值為 **False**。|  
|**日期**|具有 ISO8601 日期格式所指定之完整指定日期或日期時間值的屬性：YYYY-MM-DD[THH:MM[:SS[.S]]]。|  
|**Enum**|具有字串文字值的屬性，此文字值必須是指定值清單中的一個值。|  
|**Float**|具有浮點值的屬性。 使用句點 (.) 當做選擇性小數分隔符號。|  
|**整數**|具有整數 (int32) 值的屬性。|  
|**語言**|具有文字值的屬性，此文字值包含語言與文化特性代碼，例如「en-us」代表英文 (美國)。 該值必須是特定語言，或是在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中為其定義了預設語言的中性語言。|  
|**名稱**|具有字串文字值的屬性。 名稱在項目的命名空間中必須是唯一的。 如果未指定，項目的命名空間會是具有名稱的最內層包含物件。|  
|**NormalizedString**|具有已經正規化之字串文字值的屬性。|  
|**大小**|大小元素必須包含一個數字 (含有一個句號字元，當做選擇性小數分隔符號使用)。 這個數字必須緊接著 CSS 長度單位的指示項，例如 cm、mm、in、pt 或 pc。 數字與指示項之間的空格是選擇性的。 如需大小指示項的詳細資訊，請參閱 [CSS 值與單位參考](/previous-versions//ms537660(v=vs.85)) \(英文\)。<br /><br /> 在 RDL 中， **Size** 的最大值是 160 英吋。 大小下限是 0 英吋。|  
|**String**|具有字串文字值的屬性。|  
|**UnsignedInt**|具有不帶正負號之整數 (uint32) 值的屬性。|  
|**變數**|具有任何簡單 XML 類型的屬性。|  
  
##  <a name="rdl-data-types"></a><a name="bkmk_RDL_Data_Types"></a> RDL 資料類型  
 DataType 列舉會定義 RDL 中屬性、運算式或參數的資料類型。 下表列出說明 Common Language Runtime (CLR) 資料類型對應到 RDL 資料類型的方式。  
  
|**CLR 類型**|**對應的資料類型**|  
|-----------------------|---------------------------------|  
|Boolean|Boolean|  
|DateTime、DateTimeOffset|Datetime|  
|Int16、Int32、UInt16、Byte、SByte|整數|  
|Single、Double|Float|  
|String、Char、GUID、Timespan|String|  
  
## <a name="see-also"></a>另請參閱  
 [尋找報表定義結構描述版本 &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)   
 [將自訂組件與報表搭配使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [自訂報表項目](../../reporting-services/custom-report-items/custom-report-items.md)  
  
  
