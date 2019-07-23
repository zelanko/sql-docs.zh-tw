---
title: 比較字串資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- comparing string data
- comparison options [Integration Services]
- locales [Integration Services]
- converting string data
- string comparisons
ms.assetid: 93aeb5bd-e208-46b7-8979-dea2dcd37d4c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ca45017c7afe4b8e877018d0a121211e4eb9700e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045340"
---
# <a name="comparing-string-data"></a>比較字串資料

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  字串比較是由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]執行之許多轉換中的重要部分，此外在評估變數的運算式和屬性運算式時也會使用字串比較。 例如，「排序」轉換會比較資料集中的值，並以遞增或遞減的順序對資料進行排序。  
  
## <a name="configuring-transformations-for-string-comparisons"></a>設定字串比較的轉換  
 您可以自訂「排序」、「彙總」、「模糊群組」和「模糊查閱」轉換，以變更在資料行層級比較字串的方式。 例如，您可以指定比較忽略大小寫，這表示大寫和小寫字元都會被視為相同的字元。  
  
 下列轉換使用可包含字串比較的運算式。  
  
-   「條件式分割」轉換可使用運算式中的字串比較，以決定將資料列傳送到哪個輸出。 如需詳細資訊，請參閱 [Conditional Split Transformation](../../integration-services/data-flow/transformations/conditional-split-transformation.md)。  
  
-   「衍生的資料行」轉換可使用運算式中的字串比較，以產生新的資料行值。 如需詳細資訊，請參閱 [衍生的資料行轉換](../../integration-services/data-flow/transformations/derived-column-transformation.md)。  
  
 變數、變數對應和優先順序條件約束也使用運算式，它們可以包含字串比較。 如需運算式的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
## <a name="processing-during-string-comparison"></a>在字串比較期間處理  
 視轉換的資料和組態而定，比較字串資料的過程中可能會進行下列處理：  
  
-   將資料轉換成 Unicode。 如果來源資料還不是 Unicode，則比較發生之前資料會自動轉換成 Unicode。  
  
-   使用地區設定來套用用於解譯日期、時間、十進位資料之地區設定特定的規則和排序次序。  
  
-   在資料行層級套用比較選項來變更比較的敏感性。  
  
## <a name="converting-string-data-to-unicode"></a>將字串資料轉換成 Unicode  
 視轉換執行的作業及轉換組態而定，可以將字串資料轉換為 DT_WSTR 資料類型，這是字串字元的 Unicode 表示法。  
  
 具有 DT_STR 資料類型的字串資料，會使用資料行的字碼頁來轉換成 Unicode。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支援資料行層級的字碼頁，而每個資料行都可以用不同的字碼頁來轉換。  
  
 在大多數情況下， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可識別資料來源中的正確字碼頁。 例如，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，您可在資料庫和資料行層級設定定序。 字碼頁從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序 (可以是 Windows 或 SQL 定序) 衍生。  
  
 如果 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供一個非預期的字碼頁，或者封裝使用未提供足夠資訊來判斷字碼頁是否正確的提供者來存取資料，則您可以在 OLE DB 來源和 OLE DB 目的地中指定預設字碼頁。 此預設字碼頁會取代 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的字碼頁。  
  
 檔案不包含字碼頁。 但是，封裝用來連接到檔案資料的「一般檔案」和「多個一般檔案」連接管理員，會包含用來指定該檔案字碼頁的屬性。 字碼頁只能在檔案層級，而不能在資料行層級進行設定。  
  
## <a name="setting-locale"></a>設定地區設定  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不會使用字碼頁來推斷用於排序資料或解譯日期、時間和十進位資料之地區設定的特定規則。 反之，轉換會讀取資料流程元件、「資料流程」工作、容器或封裝上 LocaleId 屬性設定的地區設定。 依預設，轉換的地區設定會從其「資料流程」工作繼承，此工作進而從封裝繼承。 如果「資料流程」工作在某個容器中 (如「For 迴圈」容器)，則它會從容器繼承其地區設定。  
  
 您也可以指定「一般檔案」連接管理員和「多個一般檔案」連接管理員的地區設定。  
  
## <a name="setting-comparison-options"></a>設定比較選項  
 地區設定會提供比較字串資料的基本規則。 例如，地區設定指定字母表中每個字母的排序位置。 但是，這些規則對某些轉換執行的比較來說可能並不夠，而且 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 還支援一組超越地區設定之比較規則的進階比較選項。 這些比較選項可在資料行層級進行設定。 例如，其中一個比較選項可讓您忽略非空格字元。 此選項的作用是可以忽略變音符號 (例如腔調符號)，在比較時將 "a" 和 "Ã¡" 視為完全相同。  
  
 下表描述比較選項和排序樣式。  
  
|比較選項|Description|  
|-----------------------|-----------------|  
|忽略大小寫|指定比較是否區分大寫與小寫字母。 如果設定此選項，則字串比較會忽略大小寫。 例如，「ABC」與「abc」視為一樣。|  
|忽略假名類型|指定比較是否區分兩類日文的假名字元：平假名與片假名。 如果設定此選項，則字串比較會忽略假名類型。|  
|忽略字元寬度|指定比較是否區分單一位元組字元和表示為雙位元組字元的相同字元。 如果設定此選項，則字串比較會將同一字元的單一位元組表示法和雙位元組表示法視為一樣。|  
|忽略非空格字元|指定比較是否區分空格字元與變音。 如果設定此選項，則比較會忽略變音符號。 例如，"Ã¥" 等於 "a"。|  
|忽略符號|指定比較是否區分字母字元與符號 (例如空白字元、標點符號、貨幣符號和數學符號)。 如果設定此選項，則字串比較會忽略符號。 例如，" New York" 與 "New York"，以及 "*ABC" 與 "ABC"' 均被視為一樣。|  
|將標點符號當作符號來排序|指定比較是否對英數字元前面的所有標點符號進行排序 (連字號和撇號除外)。 例如，如果設定此選項，則「.ABC」將排在「ABC」前面。|  
  
 「排序」、「彙總」「模糊群組」和「模糊查閱」轉換包含這些用於比較資料的選項。  
  
 「模糊群組」和「模糊查閱」轉換的 [進階編輯器]  對話方塊中會顯示 **FullySensitive** 比較旗標。 選取 [FullySensitive]  比較旗標表示會套用所有的比較選項。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)   
 [快速剖析](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [標準剖析](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)  
  
  
