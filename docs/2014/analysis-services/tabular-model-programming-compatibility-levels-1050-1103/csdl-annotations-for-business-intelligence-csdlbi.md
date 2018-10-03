---
title: Business Intelligence (CSDLBI) 的 CSDL 註解 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: bf6f372a-bc67-45ea-a771-b2dc5b0527e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e3fa21bdf2392028ada3034c60e2525f2f657788
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055618"
---
# <a name="csdl-annotations-for-business-intelligence-csdlbi"></a>商業智慧的 CSDL 註解 (CSDLBI)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援 XML 格式中稱為「概念結構定義語言商業智慧註解」(CSDLBI) 的表格式模型定義表示法。  
  
 此主題提供 CSDLBI 的概觀，及其搭配 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料模型的用法。  
  
## <a name="understanding-the-role-of-csdl"></a>了解 CSDL 的角色  
 概念結構定義語言 (CSDL) 是一種 XML 語言，描述實體、關聯性與功能。 CSDL 會定義為實體資料架構的一部分。 BI 註解是延伸模組，其設計在於支援使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的資料模型。  
  
 雖然 CSDL 符合實體資料架構標準，但您不需要了解實體關聯性模型，也不需要任何特殊工具來建置表格式模型或以模型為基礎的報表。 您會透過使用用戶端工具 (例如 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，或像是 AMO 這類應用程式開發介面) 建立模型，並且將模型部署至伺服器。 用戶端會使用模型定義檔連接至模型，通常該檔案會發佈至可供報表設計師與報表取用者使用的 SharePoint 文件庫。 如需詳細資訊，請參閱下列連結：  
  
-   [表格式模型方案&#40;SSAS 表格式&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
-   [表格式模型方案部署&#40;SSAS 表格式&#41;](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
-   [PowerPivot BI 語意模型連接&#40;.bism&#41;](../power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)  
  
 CSDLBI 結構描述是 Analysis Services 伺服器為回應用戶端 (例如 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]) 的模型定義要求而產生的。 用戶端應用程式將 XML 查詢傳送至裝載模型資料的 Analysis Services 伺服器。 然後伺服器使用 CSDLBI 註解傳送包含模型中實體定義的 XML 訊息，以做為回應。 接著報表用戶端會使用此資訊來呈現模型中所提供的欄位、彙總以及量值。 CSDLBI 註解也會提供有關如何分組、排序與格式化資料的資訊。  
  
 如需 CSDLBI 的一般資訊，請參閱[CSDLBI 概念](csdlbi-concepts.md)。  
  
### <a name="working-with-csdl"></a>使用 CSDL  
 代表任何特定表格式模型的 CSDLBI 註解集都是 XML 文件，其中同時包含簡單和複雜的實體集合。 實體會定義包含在導出資料行、量值或 KPI 中的資料表 (或維度)、資料行 (屬性)、關聯 (關聯性) 及公式。  
  
 您無法直接修改這些物件，而必須使用專為表格式模型處理所提供的用戶端工具和應用程式開發介面 (API)。  
  
 您可以將 DISCOVER 要求傳送到裝載模型的伺服器，藉以取得模型的 CSDL。 此要求必須透過指定伺服器和模型，以及選擇性地指定檢視或檢視方塊來限定。 傳回的訊息是 XML 字串。 某些元素和語言相關，而且會根據目前連接的語言，傳回不同的值。 如需詳細資訊，請參閱 < [DISCOVER_CSDL_METADATA 資料列集](../schema-rowsets/xml/discover-csdl-metadata-rowset.md)。  
  
### <a name="csdlbi-versions"></a>CSDLBI 版本  
 原始 CSDL 規格 (來自實體資料架構) 會針對需要支援模型的多數實體和屬性提供。 BI 註解支援表格式模型的特殊需求、用戶端 (例如 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]) 所需的報表屬性，以及多維度模型所需的其他中繼資料。 本節描述每個版本中的更新。  
  
 **CSDLBI 1.0**  
  
 CSDL 結構描述的初始新增功能集，支援 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格式模型，包含可支援資料模型、自訂計算及增強呈現方式的註解。  
  
-   支援表格式模型的新元素和屬性。 例如，已加入屬性，可指定用於擴展模型的資料庫查詢類型。  
  
-   現有實體的新屬性和延伸模組。  例如，Association 元素已擴充，可支援關聯性。  
  
-   視覺效果和導覽屬性。 例如，已加入屬性，可支援自訂排序欄位、預設影像  
  
 **CSDLBI 1.1**  
  
 此版本 CSDLBI 結構描述包括可支援多維度資料庫 (例如 OLAP Cube) 的新增功能。 新元素和屬性如下：  
  
-   支援做為實體的維度。  
  
-   支援階層。  
  
-   公開 ROLAP 資料分割。  
  
-   支援翻譯。  
  
-   支援檢視方塊。  
  
 如需在 CSDLBI 註解中的個別元素的詳細資訊，請參閱[csdl 之 BI 註解的技術參考](conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)。 如需有關核心 CSDL 規格的詳細資訊，請參閱[CSDL v3 規格](https://msdn.microsoft.com/en-us/data/jj652004)MSDN 上。  
  
## <a name="see-also"></a>另請參閱  
 [了解表格式物件模型](representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [CSDLBI 概念](csdlbi-concepts.md)   
 [了解表格式物件模型](representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
