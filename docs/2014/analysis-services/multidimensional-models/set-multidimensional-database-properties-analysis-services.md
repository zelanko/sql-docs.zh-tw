---
title: 設定多維度資料庫屬性（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- properties [Analysis Services], databases
ms.assetid: a8be5b3f-3148-448a-976c-7222705155d9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aa3e1544f625183df3240359aa22b117144244d3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072997"
---
# <a name="set-multidimensional-database-properties-analysis-services"></a>設定多維度資料庫屬性 (Analysis Services)
  您[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可以在[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]資料庫設計工具中設定許多資料庫屬性。  
  
 在此設計工具中，您可以執行以下工作類型：  
  
-   如果在線上模式中連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，可以變更 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的名稱。 如果您在專案模式中工作，可以變更此資料庫名稱，以便用於下一次的專案部署。 如需詳細資訊，請參閱[重新命名多維度資料庫 &#40;Analysis Services&#41;](rename-a-multidimensional-database-analysis-services.md) 和[設定 Analysis Services 專案屬性 &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)。  
  
-   您可以提供可呈現給使用者之資料庫的描述； 您也可以檢視此資料庫的名稱，但是無法加以變更。 若要變更此資料庫名稱，您必須編輯專案的屬性。  
  
-   您可以針對一種或多種語言提供資料庫名稱和描述的翻譯。 如需詳細資訊，請參閱[Cube 翻譯](../multidimensional-models-olap-logical-cube-objects/cube-translations.md)、[維度翻譯](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)和[翻譯 &#40;Analysis Services&#41;](../translations-analysis-services.md)。  
  
-   您可以檢視及修改預設的帳戶類型對應。 當一個或多個量值使用 *ByAccount* 彙總函式時，會使用帳戶類型對應。 您可以針對每一個帳戶類型指定別名，以及修改與此帳戶類型有關的預設彙總函式。 如需修改預設彙總的詳細資訊，請參閱 [定義局部加總行為](define-semiadditive-behavior.md)。  
  
## <a name="database-properties"></a>資料庫屬性  
 除了上面提到的內容之外，您還可以在 [屬性] 視窗中設定許多資料庫屬性。  
  
|屬性|描述|  
|--------------|-----------------|  
|彙總前置詞|可用於資料庫中所有資料分割之彙總名稱的一般前置詞。 如需詳細資訊，請參閱 [AggregationPrefix 元素 &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/aggregationprefix-element-assl)。|  
|定序|當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體時，資料庫將會繼承自定序伺服器屬性，除非這裡有提供不同的值。|  
|DataSourceImpersonationInfo|針對資料庫中的所有資料來源物件指定預設模擬模式， 這是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務在處理物件、同步處理伺服器，以及執行 OpenQuery 和 SystemOpenSchema 資料採礦陳述式時所用的模式。|  
|估計的大小|提供磁碟上資料庫檔案的預估大小。 如果資料儲存在多個位置，此預估值僅限於儲存在資料庫資料夾底下的資料檔案。<br /><br /> 
  `EstimatedSize` 也可以當做預估記憶體的基礎使用。 一般來說，記憶體需求會大於磁碟資料大小，因為將資料庫載入記憶體時會產生額外的資料結構。<br /><br /> 若要進一步預估記憶體需求，您也可以使用工作管理員，在處理資料庫前後查看 Analysis Services 處理序記憶體，並觀察耗用的記憶體，當做了解資料庫之記憶體需求的方法。|  
|Language|當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體時，資料庫將會繼承自語言伺服器屬性，除非這裡有提供不同的值。|  
|MasterDataSource ID|與遠端資料分割一起使用。 如需詳細資訊，請參閱 [遠端資料分割](../multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSAS-多維度&#41;的 [資料庫屬性] 對話方塊](../database-properties-dialog-box-ssas-multidimensional.md)   
 [設定 Analysis Services 專案屬性 &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)  
  
  
