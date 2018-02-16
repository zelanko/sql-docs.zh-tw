---
title: "資料來源中產生非時間資料表來建立維度 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- data sources [Analysis Services], dimensions without data source
- dimensions [Analysis Services], standard
- dimensions [Analysis Services], creating without data source
- standard dimensions [Analysis Services]
ms.assetid: a37f7a46-7451-4582-ba19-2595196d97bc
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dda2fe632e3a4cae0f36d766d4778f5ff910d649
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="create-a-dimension-by-generating-a-non-time-table-in-the-data-source"></a>在資料來源中產生非時間資料表來建立維度
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的 [維度精靈] 建立維度，而不需使用現有的資料來源。 方法是，選取精靈之 [選取建立方法] 頁面的 [在資料來源中產生非時間資料表] 選項。 若要在基礎資料來源中建立新的維度資料表，您必須擁有在基礎資料來源中建立物件的權限。 在沒有預先定義之資料來源檢視的情況下定義維度時，可以從頭開始定義維度或使用維度範本。  
  
 「維度精靈」提供了一些維度範本範例，讓您可以建立常見的維度類型。 您可以從以下維度類型中選擇：  
  
-   帳戶  
  
-   客戶  
  
-   日期  
  
-   部門  
  
-   目的地貨幣  
  
-   員工  
  
-   Geography  
  
-   網際網路銷售訂單的詳細資料  
  
-   組織  
  
-   產品  
  
-   促銷  
  
-   轉售商銷售訂單的詳細資料  
  
-   轉售商  
  
-   銷售通路  
  
-   銷售原因  
  
-   銷售摘要訂單的詳細資料  
  
-   銷售地區  
  
-   狀況  
  
-   來源貨幣  
  
 每個標準範本都支援可供選擇納入維度的屬性。 您也可以針對資料常用到的維度，加入自己的範本檔案。 維度範本位於以下資料夾：  
  
 `C:\Program Files\Microsoft SQL Server\100\Tools\Templates\olap\1033\Dimension Templates`  
  
 您可以在完成「維度精靈」之後，使用 [維度設計師] 在維度中加入、移除和設定屬性與階層。  
  
 在不使用資料來源的情況下建立非時間維度時，「維度精靈」會引導您透過下列步驟，指定維度類型並識別索引鍵屬性和緩時變維度。  
  
## <a name="specify-dimension-type"></a>指定維度類型  
 在 [維度精靈] 的 [指定維度類型] 頁面上，您可以指定維度類型。 如果您要以範本為基礎建立維度，就會為您定義維度類型。 您也可以在此頁面上選取指定之維度類型的標準屬性 (如果有的話)。  
  
 如果您選取的範本對應到維度類型，此頁面會使用該維度類型的選項擴展。 如果您並未選取範本，或沒有對應的維度類型，預設的維度類型為 [一般]。 如果尚未選取維度類型，請為您建立的維度選取最適當的類型。 如果沒有為 [維度類型] 列出的適當類型，請使用 [一般]。  
  
 選取維度類型時，精靈會在 [維度屬性] 下，列出適用於此維度的屬性類型。 若要選取屬性類型，請選取該屬性類型旁的 [包含] 核取方塊，再於 [維度屬性] 下輸入屬性的名稱。 預設名稱與 [屬性類型] 相同。  
  
## <a name="identify-key-attribute-and-changing-dimensions"></a>識別索引鍵屬性與變更維度  
 在 [指定維度索引鍵和類型] 頁面上，選取要作為維度之索引鍵屬性的屬性。 索引鍵屬性通常會對應到主維度資料表的主索引鍵資料行，並索引維度的分葉成員。  
  
 如果您選取範本，而且在範本中有定義索引鍵屬性，則該屬性為預設索引鍵屬性。 如果您選取範本，但是在範本中沒有定義索引鍵屬性，則預設值為清單中的第一個屬性。 此清單包含您在 [指定維度類型] 頁面上選取的所有屬性。 您可以選取您在 [指定維度類型] 頁面上選取的任何屬性，作為索引鍵屬性。 如果您並未選取任何屬性，精靈會自動建立索引鍵屬性，並串連維度名稱與「識別碼」來為其命名。  
  
 最後，指定此維度是否為變更維度。 變更維度中的成員會隨著時間而移至階層內的不同位置。 精靈會產生其他資料行並建立對應到這些資料行的屬性。 這些資料行將會讓使用者以變更中之因數的方式，查詢維度。 之後使用「結構描述產生精靈」建立的任何封裝，都會根據維度的緩時變維度特性來管理 Surrogate 索引鍵。  
  
 當您選取 [這是變更維度] 核取方塊時，[維度精靈] 會定義下表中指出的屬性：  
  
|Attribute|型別|  
|---------------|----------|  
|SCD OriginalID|SCDOriginalID|  
|SCD 結束日期|SCDEndDate|  
|SCD 開始日期|SCDStartDate|  
|SCD 狀態|SCDStatus|  
  
 如果您使用的範本中有定義這些緩時變維度屬性，預設會選取 [這是變更維度] 核取方塊。 如果您清除核取方塊，則會從維度中移除緩時變維度屬性。  
  
 您可以使用維度設計師來設定緩時變維度的屬性。  
  
## <a name="completing-the-dimension-wizard"></a>完成維度精靈  
 在 [正在完成精靈] 頁面上，輸入新維度的名稱，然後檢視維度結構。 選取 [立即產生結構描述] 核取方塊，在您按一下 [完成] 後即可啟動 [結構描述產生精靈]。 在大多數情況下，如果您計畫建立其他物件，則不應選取此核取方塊。 如果您並未選取此核取方塊，也可在稍後使用維度設計師來產生結構描述。  
  
## <a name="see-also"></a>另請參閱  
 [產生時間資料表來建立時間維度](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [產生時間資料表來建立時間維度](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)  
  
  
