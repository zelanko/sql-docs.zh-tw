---
title: SQL Server 版本的計算容量限制 | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- processors [SQL Server], supported
- number of processors supported
- maximum number of processors supported
ms.assetid: cd308bc9-9468-40cc-ad6e-1a8a69aca6c8
caps.latest.revision: 60
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 50adedb266ef265f7e829826bb4acc54cd60dfbb
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="compute-capacity-limits-by-edition-of-sql-server"></a>SQL Server 版本的計算容量限制
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本文討論 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本的計算容量限制，及其在具有超執行緒處理器的實體和虛擬化環境中有何差異。  
  
 ![對應至計算容量限制](../sql-server/media/compute-capacity-limits.gif "對應至計算容量限制")  
  
 下表說明上圖中的標記法：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|0..1|零個或一個|  
|@shouldalert|只有一個|  
|1..\*|一個或多個|  
|0..\*|零個或多個|  
|1..2|一個或兩個|  
  
> [!IMPORTANT]  
> 詳細說明：  
>   
> - 一個虛擬機器 (VM) 會配有一或多個虛擬處理器。  
> - 一個或多個虛擬處理器只會配置給一個虛擬機器。  
> - 零個或一個虛擬處理器會對應至零個或多個邏輯處理器。 當虛擬處理器與邏輯處理器之間的對應為： 
>     -   一對零，表示客體作業系統未使用未繫結邏輯處理器。  
>     -   一對多，表示過度認可。  
>     -   零對多，表示虛擬機器不在主機系統上。 因此 VM 未使用任何邏輯處理器。  
> - 一個插槽會對應至零個或多個核心。 當插槽與核心之間的對應為：  
>     -   一對零，表示空的插槽。 未安裝任何晶片。  
>     -   一對一，表示插槽內裝有單核晶片。 這種對應目前不多。  
>     -   一對多，表示插槽內裝有多核晶片。 典型值為 2、4 和 8。  
> - 一個核心會對應至一個或兩個邏輯處理器。 當核心與邏輯處理器之間的對應為：  
>     -   一對一，表示超執行緒已關閉。  
>     -   一對二，表示超執行緒已開啟。  
  
 下列定義適用於本文所用的詞彙：  
  
-   就 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、作業系統、應用程式或驅動程式的角度而言，執行緒或邏輯處理器皆為一種邏輯運算引擎。  
  
-   核心則是處理器單元， 可能由一或多個邏輯處理器組成。  
  
-   一個實體處理器可能是由一個或多個核心組成。 實體處理器與處理器套件或插槽相同。  
  
具有多個實體處理器的系統或是具有多核心及/或超執行緒之實體處理器的系統可讓作業系統同時執行多個工作。 每個執行的執行緒都會顯示成邏輯處理器。 例如，如果您的電腦具有兩個啟用超執行緒的四核心處理器，且每個核心都有兩個執行緒，則一共有 16 個邏輯處理器：2 個處理器 x 每個處理器 4 個核心 x 每個核心 2 個執行緒。 值得注意的是：  
  
-   來自超執行緒核心之單一執行緒的邏輯處理器計算容量小於來自停用超執行緒之相同核心的邏輯處理器計算容量。  
  
-   超執行緒核心中兩個邏輯處理器的計算容量則大於停用超執行緒之相同核心的計算容量。  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的每個版本都有兩個計算容量限制：  
  
- 插槽 (或實體處理器或處理器套件) 數目上限  
  
- 作業系統所報告的核心數目上限  
  
這些限制適用於單一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體。 它們代表單一執行個體將會使用的計算容量上限。 並不會限制要部署執行個體的目標伺服器。 實際上，在相同的實體伺服器上部署 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的多個執行個體可以有效使用插槽及 (或) 核心數目超過允許容量限制的實體伺服器計算容量。  
  
下表指定每個 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]版本之單一執行個體的計算容量限制：  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|單一執行個體的計算容量上限 ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)])|單一執行個體的計算容量上限 (AS、RS)|  
|---------------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
|Enterprise Edition：核心授權\*|作業系統最大值|作業系統最大值|  
|Developer|作業系統最大值|作業系統最大值|  
|Standard|限制為 4 個插槽或 24 個核心的較小者|限制為 4 個插槽或 24 個核心的較小者|  
|Express|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|  

\*伺服器與用戶端存取使用權 (CAL) 的 Enterprise Edition 授權限制為每個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體 20 個核心。 (新協議未提供此授權。)核心伺服器授權模式之下沒有任何限制。  
  
在虛擬環境中，計算容量限制的依據為邏輯處理器的數目，而非核心數目。 原因是客體應用程式看不見處理器架構。 

例如，如果一部伺服器的四個插槽都插入四核心處理器，而且能夠為每個核心啟用兩個超執行緒，則在啟用超執行緒的情況下，總共包含 32 個邏輯處理器。 但是在停用超執行緒的情況下，只包含 16 個邏輯處理器。 這些邏輯處理器可對應至伺服器上的虛擬機器。 而該邏輯處理器的虛擬機器計算負載則對應至主機伺服器中實體處理器上執行的執行緒。  
  
當每個虛擬處理器的效能都很重要時，建議您停用超執行緒。 您可以在 BIOS 設定期間，使用處理器的 BIOS 設定啟用或停用超執行緒。 但是，超執行緒通常是伺服器範圍的作業，會影響到在伺服器上執行的所有工作負載。 因此，建議您分隔在虛擬環境中執行的工作負載與實體作業系統環境中可從超執行緒效能獲益的工作負載。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2016 的版本和元件](../sql-server/editions-and-components-of-sql-server-2016.md)   
 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [SQL Server 的最大容量規格](../sql-server/maximum-capacity-specifications-for-sql-server.md)   
 [SQL Server 2016 的安裝快速入門](http://msdn.microsoft.com/library/672afac9-364d-4946-ad5d-8a2d89cf8d81)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
