---
title: 建立日期類型維度 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time dimensions [Analysis Services]
- dimensions [Analysis Services], time
- adding time intelligence
- server time dimensions [Analysis Services]
- calendars [Analysis Services]
- time intelligence [Analysis Services]
ms.assetid: 6d692856-4b01-4dca-a650-f97ac220c114
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3eec8ddf87193eddbafc5a56e8e397c83f142a91
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513067"
---
# <a name="create-a-date-type-dimension"></a>建立日期類型維度
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，時間維度是其屬性代表時間週期的維度類型，例如年、學期、季、月和日。 時間維度中的週期，會為分析和報表提供時間層級的資料粒度。 屬性會組織在階層中，而時間維度的資料粒度多半取決於記錄資料的商務和報表需求。 例如，商業智慧應用程式中的大部份財務和商務資料，都使用每月或每季的資料粒度。  
  
 通常， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的 Cube 會將時間維度併入某個表單或其他表單中。 Cube 可能會包含多個時間維度，或來自相同時間維度的數個階層，視資料的資料粒度和報表需求而定。 不過，並非所有 Cube 都需要時間維度。 因為活動式維度的成本估計是根據活動，而非時間，所以有些 OLAP 應用程式 (例如活動式成本估計) 並不需要時間維度。  
  
## <a name="dimension-structure"></a>維度結構  
 時間維度的維度結構，會視基礎資料來源如何儲存時間週期資訊而定。 儲存方式的差異會產生兩種基本類型的時間維度：  
  
 時間維度  
 時間維度與其他維度類似，因為維度資料表會提供維度的屬性。 維度主資料表的每一個資料行，會定義特定時間週期的屬性。  
  
 與其他維度類似，事實資料表與時間維度的維度資料表具有外部索引鍵關聯性。 時間維度的索引鍵屬性，是以整數索引鍵為基礎或最低層級的詳細資料為基礎，例如會出現在維度主資料表中的日期。  
  
 伺服器時間維度  
 如果您沒有可繫結與時間相關之屬性的維度資料表，可以讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 根據時間週期來定義伺服器時間維度。 若要定義伺服器時間維度所代表的階層、層級和成員，您可在建立維度時選取標準時間週期。  
  
 伺服器時間維度中的屬性具有特定的時間屬性繫結。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用與日期相關的屬性類型 (例如年、月或日) 來定義時間維度中的屬性成員。  
  
 在 Cube 中包含伺服器時間維度之後，您可以在 Cube 精靈的 [定義維度使用方式] 頁面上指定關聯性，來設定量值群組和伺服器時間維度之間的關聯性。  
  
### <a name="calendars"></a>日曆  
 在時間維度或伺服器時間維度中，會在階層中將時間週期屬性加以分組。 這種階層通常稱為日曆。  
  
 商業智慧應用程式通常會需要多個日曆定義。 例如，人力資源部門時，可能會使用追蹤員工*標準*行事曆的 12 個月的西曆年 1 月 1 日開始年 12 月 31 日結束。 不過，該相同的人力資源部門時，可能會使用追蹤支出*會計*行事曆的 12 個月日曆，用以定義組織所使用的會計年度。  
  
 您可以在維度設計師中，手動建構這些不同的日曆。 不過，維度精靈有提供數個階層範本，當您建立時間維度或伺服器時間維度時，可以使用這些範本來自動產生數種類型的日曆。 下表描述可由維度精靈產生的各種日曆。  
  
|行事曆|描述|  
|--------------|-----------------|  
|標準日曆|12 個月的西曆，從 1 月 1 日開始，到 12 月 31 日結束。<br /><br /> 不論您使用維度精靈來建立時間維度或伺服器時間維度，在您定義代表維度時間週期的屬性之後，精靈都會產生標準日曆的階層。 如果您使用維度精靈來建立伺服器時間維度，您可以調整標準日曆的起始日期，成為從 1 月 1 日以外的日期開始。|  
|會計日曆|十二月份會計日曆。 當您選取此日曆時，請指定組織所使用會計年度起始日期和月份。<br /><br /> 注意：唯有使用維度精靈建立伺服器時間維度時，才能使用這個日曆。|  
|報表日曆(或行銷日曆)|12 個月的報表日曆，包含兩個四週的月份以及一個五週的月份，且每三個月 (每季) 重複一次的模式。 當您選取此日曆時，指定起始的日期和月份，以及 4-4-5、 4-5-4 或 5-4-4 週，其中每一個數字代表一個月的週數的三個月模式。<br /><br /> 注意：唯有使用維度精靈建立伺服器時間維度時，才能使用這個日曆。|  
|製造日曆|使用 13 週期 (每一期四週) 的日曆，分成三個週期三季和四個週期一季。 當您選取這個日曆時，請指定您組織所採用製造年的起始週 (在 1 和 4 之間) 和月份，也請找出哪一季要包含四個週期。<br /><br /> 注意：唯有使用維度精靈建立伺服器時間維度時，才能使用這個日曆。|  
|ISO 8601 日曆|日期和時間標準日曆 (8601) 的國際標準組織 (ISO) 表示法。 此日曆含有 7 天一週的整數。 新的年份可以在西曆的新年之前幾天或之後幾天開始。 此日曆的第一週，是由西曆包含星期四的第一週。 因此，本週的第一天 (星期日)有可能會出現在上一個年份。<br /><br /> 注意：唯有使用維度精靈建立伺服器時間維度時，才能使用這個日曆。|  
  
 當您建立伺服器時間維度，並指定在該維度使用的時間週期和日曆時，維度精靈會為每一個指定的日曆，加入適當的時間週期屬性。 例如，如果您建立使用年份做為時間週期的伺服器時間維度，並同時包含會計和報表日曆，則精靈會將 FiscalYear 和 ReportingYears 屬性以及標準的 Year 屬性都加入維度中。 伺服器時間維度也會有所選取時間週期的組合之屬性，例如包含 Days 和 Weeks 之維度的 DayOfWeek 屬性。 維度精靈會藉由結合屬於單一日曆類型的屬性，來建立日曆階層。 例如，會計日曆階層可能包含下列層級：會計年度、 會計半年、 會計季度、 會計月和會計日。  
  
## <a name="adding-time-intelligence-with-the-business-intelligence-wizard"></a>使用商業智慧精靈加入時間智慧  
 在定義時間維度並將該維度加入至 Cube 之後，您可以使用商業智慧精靈來加入時間智慧功能，例如某週期至今、某週期至另一週期和滾動平均量值。 如需詳細資訊，請參閱 [使用商業智慧精靈定義時間智慧計算](define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)。  
  
> [!NOTE]  
>  您不能使用商業智慧精靈將時間智慧加入至伺服器時間維度。 商業智慧精靈會加入支援時間智慧的階層，而此階層必須繫結到時間維度資料表的資料行。 伺服器時間維度沒有對應的時間維度資料表，因此無法支援此額外階層。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Time Dimension by Generating a Time Table](create-a-time-dimension-by-generating-a-time-table.md)   
 [商業智慧精靈 F1 說明](../business-intelligence-wizard-f1-help.md)   
 [維度類型](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
