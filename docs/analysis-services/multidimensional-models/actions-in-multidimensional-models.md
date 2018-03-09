---
title: "多維度模型中的動作 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- actions [Analysis Services], creating
- report actions [Analysis Services]
- drillthrough actions [Analysis Services]
- cubes [Analysis Services], actions
ms.assetid: b9fee2b9-05a5-4077-848d-d8457326dc27
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6c68c3d8eba2ec1519c38a89c7a1b0b71f3be4e3
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="actions-in-multidimensional-models"></a>多維度模型中的動作
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
動作是使用者在所選取的 Cube 或部分 Cube 上所起始的作業。 這個作業可以使用所選取項目做為參數來啟動應用程式，或擷取關於所選取項目的資訊。 如需動作的詳細資訊，請參閱[動作 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
 使用 Cube 設計師的 [動作] 索引標籤來建立 Cube 的動作。 指定下列項目：  
  
 **名稱**  
 選取用來識別動作的名稱。  
  
 **動作目標**  
 選取動作所附加的對象物件。 一般而言，在用戶端應用程式中，當使用者選取目標物件時便會顯示動作；但是，用戶端程式會決定哪一個使用者作業顯示動作。 若為 [目標類型]，請從下列物件中選取：  
  
-   屬性成員  
  
-   資料格  
  
-   Cube  
  
-   維度成員  
  
-   階層  
  
-   階層成員  
  
-   Level  
  
-   層級成員  
  
 選取目標物件類型之後，在 [目標物件] 下，選取指定類型的 Cube 物件。  
  
 **條件 (選擇性)**  
 指定解析成布林值的選擇性多維度運算式 (MDX) 運算式。 如果值為 **True**，就會在指定的目標上執行動作。 如果值為 **False**，則不會執行動作。  
  
 **動作內容**  
 選取動作的類型。 下表摘要可以使用的類型。  
  
|型別|Description|  
|----------|-----------------|  
|資料集|擷取資料集。|  
|專屬|使用不同於此資料表列出的介面來執行作業。|  
|資料列集|擷取資料列集。|  
|Statement|執行 OLE DB 命令。|  
|URL|在網際網路瀏覽器中顯示變數網頁。|  
  
 若為 [動作運算式]，指定執行動作時會傳遞的參數。 語法必須評估為字串，而且必須包含以 MDX 撰寫的運算式。 例如，您的 MDX 運算式可以表示語法中所包含之 Cube 的一部分。 在傳遞參數之前會先評估 MDX 運算式。 另外，MDX 產生器可以協助您建立 MDX 運算式。  
  
 **其他屬性**  
 選取屬性。 下表摘要可以使用的屬性。  
  
|屬性|Description|  
|--------------|-----------------|  
|**引動過程**|指定動作如何執行。 預設為互動式，會指定使用者存取物件時執行的動作。 可能的設定有：<br /><br /> 批次<br /><br /> 互動式<br /><br /> 開啟時|  
|**應用程式**|描述動作的應用程式。|  
|**說明**|描述動作。|  
|**Caption**|提供為動作顯示的標題。 如果標題是 MDX，請將 [標題是 MDX] 指定為 **True**。|  
|**標題是 MDX**|如果標題是 MDX，請指定 **True** ；如果不是 MDX，則指定 **False** 。|  
  
> [!NOTE]  
>  您必須使用 Analysis Services 指令碼語言 (ASSL) 或分析管理物件 (AMO) 來定義 HTML 和命令列動作類型。 如需詳細資訊，請參閱 [Action 元素 &#40;ASSL&#41;](../../analysis-services/scripting/objects/action-element-assl.md)、[Type 元素 &#40;Action&#41; &#40;ASSL&#41;](../../analysis-services/scripting/properties/type-element-action-assl.md) 和[設計 AMO OLAP 進階物件的程式](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-advanced-objects.md)。  
  
## <a name="creating-a-reporting-action"></a>建立報表動作  
 報表伺服器會回應以 URL 為基礎的報表要求。 若要建立報表動作，請在 [Cube] 功能表上，按一下 [新增報表動作]。 下列選項是報表動作特有的選項。  
  
 **報表伺服器**  
 下表中描述的屬性是為報表伺服器指定的。  
  
|屬性|Description|  
|--------------|-----------------|  
|**伺服器名稱**|正在執行報表伺服器的電腦名稱。|  
|**伺服器路徑**|報表伺服器所公開的路徑。|  
|**報表格式**|HTML5、HTML3、Excel 或 PDF。|  
  
> [!NOTE]  
>  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，您可以在伺服器名稱屬性中指定傳輸層安全性 (https:)。  
  
 **參數 (選擇性)**  
 建立動作時，會將參數傳送到伺服器做為 URL 字串的一部分。 這些參數包括 [參數名稱] 和 [參數值]，後者為 MDX 運算式。  
  
 報表伺服器 URL 的建構如下：  
  
```  
  
http://  
host  
/  
virtualdirectory  
/Path&  
parametername1  
=  
parametervalue1  
& ...  
```  
  
 例如：  
  
```  
http://localhost/ReportServer/Sales/YearlySalesByCategory?rs:Command=Render&Region=West  
```  
  
## <a name="creating-a-drillthrough-action"></a>建立鑽研動作  
 鑽研動作是由資料列集動作定義的，會傳回到用戶端應用程式做為鑽研陳述式。 動作目標是量值群組的成員。 若要建立新的鑽研動作，請在 [Cube] 功能表上，按一下 [新增鑽研動作]。 下列選項是鑽研動作特有的選項：  
  
 **鑽研資料行**  
 選取一或多個維度，並針對每一個維度，選取由動作傳回到用戶端應用程式的鑽研資料行。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的 cube](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
