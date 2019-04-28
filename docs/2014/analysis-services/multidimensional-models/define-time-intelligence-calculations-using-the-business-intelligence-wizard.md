---
title: 定義時間智慧計算使用商業智慧精靈 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- period over period growth [Analysis Services]
- parallel period comparisons [Analysis Services]
- Business Intelligence enhancements [Analysis Services], time intelligence
- time views [Analysis Services]
- hierarchies [Analysis Services], time
- time periods [Analysis Services]
- moving averages
- time [Analysis Services]
- period to date [Analysis Services]
- calculations [Analysis Services], time
- time hierarchies [Analysis Services]
- time intelligence [Analysis Services]
ms.assetid: be36e8fc-f46e-4553-8623-b27d695c330b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a67270205e6c6977e01c274f0f864dc77ce8b13
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726422"
---
# <a name="define-time-intelligence-calculations-using-the-business-intelligence-wizard"></a>使用商業智慧精靈定義時間智慧計算
  時間智慧增強功能是一種 Cube 增強功能，用於將時間計算 (時間檢視) 加入至選取的階層。 此增強功能支援下列計算類別目錄：  
  
-   至今的期間數。  
  
-   期間的成長。  
  
-   移動平均。  
  
-   平行期間比較。  
  
 您將時間智慧套用到具有時間維度的 Cube。 (時間維度是 `Type` 屬性設成 `Time` 的維度)。 另外，該維度時間屬性的， `Type` 屬性，也必須有適當的設定 (例如，年份或月份)。 如果您使用維度精靈來建立時間維度，維度及其屬性的 `Type` 屬性都會正確地設定。  
  
 若要將時間智慧加入 Cube，您可使用 [商業智慧精靈]，並於 [選擇增強功能] 頁面上選取 [定義時間智慧] 選項。 然後，此精靈會引導您逐步完成選取要加入時間智慧的階層，並在將會套用時間智慧的階層內指定成員。 在精靈的最後一頁，您可以查看加入選取的時間智慧後，將會對 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫進行的變更。  
  
## <a name="selecting-a-time-hierarchy"></a>選取時間階層  
 在 [選擇目標階層與計算] 頁面上，您可以選取時間增強功能套用的時間階層。 每一次執行商業智慧精靈時，您只可以套用時間增強功能到一個時間階層。 如果您要套用增強功能到多個時間階層，就要再次執行精靈。  
  
 選取時間階層後，在 [可用的時間計算] 清單中，您可選取套用至階層的計算。 根據階層中的層級與針對每個層級之屬性的 `Type` 屬性設定，決定列出的計算。 例如，年度階層支援年初至今與年的成長，但是季階層則否。  
  
> [!NOTE]  
>  Timeintelligence.xml 範本檔案定義 [可用的時間計算] 中列出的時間計算。 如果列出的計算不符合您的需求，您可以變更現有的計算，或將新的計算加入 Timeintelligence.xml 檔案中。  
  
> [!TIP]  
>  若要檢視計算的描述，請使用向上與向下箭號以反白顯示該計算。  
  
## <a name="apply-time-views-to-members"></a>將時間檢視套用至成員  
 在 [定義計算範圍] 頁面上，您可以指定要套用新時間檢視的成員。 您可將新時間檢視套用到下列物件之一：  
  
-   **帳戶維度的成員**：在 [定義計算範圍] 頁面上，[可用的量值] 清單中包含帳戶維度。 帳戶維度之 `Type` 屬性設定成 `Accounts`。 如果您有帳戶維度，但該維度並未在 [可用的量值] 清單中顯示，您可以使用 [商業智慧精靈] 將帳戶智慧套用至該維度。 如需詳細資訊，請參閱[將帳戶智慧加入至維度中](bi-wizard-add-account-intelligence-to-a-dimension.md)。  
  
-   **量值** ：您可以指定時間檢視套用的量值，而非指定帳戶維度。 在此狀況下，請選取所選的時間計算套用的檢視。 例如，資產和負債是年度至今的資料；因此，您不會將年度至今計算套用到資產或負債量值。  
  
## <a name="viewing-the-time-intelligence-enhancement"></a>檢視時間智慧增強功能  
 在 [商業智慧精靈] 的最後一頁，您可以檢視將會對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫進行的變更。 針對時間智慧增強功能，精靈會變更選取的時間維度、關聯的資料來源檢視以及關聯的 Cube，如下表所述。  
  
|Object|變更|  
|------------|------------|  
|時間維度|針對每個計算 (或檢視) 加入屬性。|  
|資料來源檢視|針對時間維度中的每個新屬性，在時間資料表內加入導出資料行。|  
|Cube|加入定義多維度運算式 (MDX) 程式碼的導出成員以執行計算。|  
  
## <a name="see-also"></a>另請參閱  
 [建立導出成員](create-calculated-members.md)  
  
  
