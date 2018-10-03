---
title: 運算式中的內建集合 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 78d5e3b8-9320-4e4b-a025-e2de3cf7afa7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 6065291efcf59f5ac5341b47bfdae95afb35a119
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095658"
---
# <a name="built-in-collections-in-expressions-report-builder-and-ssrs"></a>運算式中的內建集合 (報表產生器及 SSRS)
  在報表的運算式中，您可以包含下列內建集合的參考：ReportItems、Parameters、Fields、DataSets、DataSources、Variables，以及類似報表名稱等全域資訊的內建欄位。 並不是所有的集合都會顯示在 **[運算式]** 對話方塊中。 只有報表伺服器上已發行的報表，才可以在執行階段使用 DataSets 和 DataSources 集合。 ReportItems 集合是報表區域中的文字方塊集合，例如在頁面或頁首中的文字方塊。  
  
 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Collections"></a> 了解內建集合  
 下表列出可在撰寫運算式時使用的內建集合。 每一列都包含該集合的區分大小寫程式設計名稱，以及您是否可以使用 [運算式] 對話方塊以互動的方式加入集合的參考、範例及描述 (包含初始化及提供集合值的時間)。  
  
|內建集合|[運算式] 對話方塊中的類別目錄|範例|描述|  
|--------------------------|-------------------------------------------|-------------|-----------------|  
|`Globals`|內建欄位|`=Globals.ReportName`<br /><br /> `- or -`<br /><br /> `=Globals.PageNumber`|代表對報表很有用的全域變數，例如：報表名稱或頁碼。 永遠可以使用。<br /><br /> 如需詳細資訊，請參閱[內建的全域和使用者參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-built-in-globals-and-users-references-report-builder.md)。|  
|`User`|內建欄位|`=User.UserID`<br /><br /> - 或 -<br /><br /> `=User.Language`|代表有關執行報表之使用者的資料集合，例如，語言設定或使用者識別碼。 永遠可以使用。<br /><br /> 如需詳細資訊，請參閱[內建的全域和使用者參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-built-in-globals-and-users-references-report-builder.md)。|  
|`Parameters`|參數|`=Parameters("ReportMonth").Value`<br /><br /> - 或 -<br /><br /> `=Parameters!ReportYear.Value`|代表報表參數的集合，每個參數都可以是單一值或多重值。 處理初始化完成後才可以使用。 如需詳細資訊，請參閱[參數集合參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)。|  
|`Fields(` *\<資料集 >* `)`|欄位|`=Fields!Sales.Value`|代表可供報表使用之資料集的欄位集合。 可在從資料來源將資料擷取至資料集之後使用。 如需詳細資訊，請參閱[資料集 Fields 集合參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-dataset-fields-collection-references-report-builder.md)。|  
|`DataSets`|不顯示|`=DataSets("TopEmployees").CommandText`|代表從報表定義的主體所參考的資料集集合。 不包含只用於頁首或頁尾的資料來源。 不適用於本機預覽。 如需詳細資訊，請參閱 [DataSources 和 DataSets 集合參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-datasources-and-datasets-references-report-builder.md)。|  
|`DataSources`|不顯示|`=DataSources("AdventureWorks2012").Type`|代表從報表主體內所參考的資料來源集合。 不包含只用於頁首或頁尾的資料來源。 不適用於本機預覽。 如需詳細資訊，請參閱 [DataSources 和 DataSets 集合參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-datasources-and-datasets-references-report-builder.md)。|  
|`Variables`|`Variables`|`=Variables!CustomTimeStamp.Value`|代表報表變數和群組變數的集合。 如需詳細資訊，請參閱[報表和群組變數集合參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md)。|  
|`ReportItems`|不顯示|`=ReportItems("Textbox1").Value`|代表報表項目的文字方塊集合。 這個集合可以用來摘要頁面上的項目，以包含在頁首或頁尾中。 如需詳細資訊，請參閱 [ReportItems 集合參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-reportitems-collection-references-report-builder.md)。|  
  
##  <a name="Syntax"></a> 在運算式中使用集合語法  
 若要從運算式參考集合，您可以針對集合中的項目使用標準 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 語法。 下表顯示集合語法的範例。  
  
|語法|範例|  
|------------|-------------|  
|*Collection!ObjectName.Property*|`=Fields!Sales.Value`|  
|*Collection!ObjectName("屬性")*|`=Fields!Sales("Value")`|  
|*Collection("物件名稱").Property*|`=Fields("Sales").Value`|  
|*Collection("成員")*|`=User("Language")`|  
|*Collection.Member*|`=User.Language`|  
  
## <a name="see-also"></a>另請參閱  
 [新增運算式&#40;報表產生器及 SSRS&#41;](add-an-expression-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
