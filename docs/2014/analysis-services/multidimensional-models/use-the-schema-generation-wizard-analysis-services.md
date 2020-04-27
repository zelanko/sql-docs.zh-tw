---
title: 使用架構產生嚮導（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Schema Generation Wizard, steps
- relational schema [Analysis Services], Schema Generation Wizard
ms.assetid: 8c710745-d41d-4c31-b6a2-2956229df75a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e434493813f0237533ca2e50ff089974f3556f34
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66072649"
---
# <a name="use-the-schema-generation-wizard-analysis-services"></a>使用結構描述產生精靈 (Analysis Services)
  結構描述產生精靈在產生階段，需要不多的資訊。 [結構描述產生精靈] 產生關聯式結構描述所需的大部分資訊，都是從您在專案中已建立的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube 和維度中擷取。 此外，您可以自訂產生主題領域資料庫結構描述的方式，以及為結構描述中之物件命名的方式。  
  
## <a name="start-the-wizard"></a>啟動精靈  
 您可以使用幾個不同的方法從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 開啟 [結構描述產生精靈]：  
  
-   以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案物件，然後從內容功能表按一下 [產生關聯式結構描述]****。  
  
-   按一下 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案物件，然後從 [資料庫]**** 功能表按一下 [產生關聯式結構描述]****。  
  
-   按一下精靈最後一頁上的 [立即產生結構描述]**** 核取方塊，從 [維度精靈] 內啟動精靈。  
  
## <a name="step-1-specify-targets"></a>步驟 1：指定目標  
 您必須指定您希望 [結構描述產生精靈] 在其中產生主題領域資料庫之結構描述的資料來源檢視 (DSV)。 雖然您可以選取現有的 DSV，不過通常是會根據資料來源建立新的 DSV。 您可以根據現有的或新的連接，或是根據另一個物件，來建立資料來源。 [結構描述產生精靈] 會在資料來源及資料來源檢視所參考的資料庫中，為主題領域資料庫產生結構描述。 [結構描述產生精靈] 不會建立主題領域資料庫本身，而是會建立關聯式結構描述來支援您所指定之現有資料庫中的 Cube 和維度。  
  
 [結構描述產生精靈] 產生基礎物件時，會使用來源檢視樣式繫結，將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 維度和 Cube 繫結到產生的資料表與資料行。  
  
> [!NOTE]  
>  若要解除 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 維度和 Cube 與先前產生之物件之間的繫結，請刪除 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube 和維度所繫結的資料來源檢視，然後使用 [結構描述產生精靈]，為 Cube 和維度定義新的資料來源檢視。  
  
## <a name="step-3-specify-schema-options-for-the-subject-area-database"></a>步驟 3：指定主題領域資料庫的結構描述選項  
 [結構描述產生精靈] 提供許多選項，可以定義為主題領域資料庫產生的結構描述。 您可以在精靈的 [主題領域資料庫結構描述選項]**** 頁面上，指定這些選項。  
  
### <a name="specifying-the-schema-owner"></a>指定結構描述擁有者  
 您可以將 [主控結構描述]**** 的值設定為有效的字串，以指定結構描述的擁有者。 結構描述的預設擁有者是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，不過您可以指定任何想要的結構描述擁有者。  
  
### <a name="specifying-primary-keys-indexes-and-constraints"></a>指定主索引鍵、索引和條件約束  
 依預設，結構描述產生精靈會在主題領域資料庫裡的每個維度資料表中，建立一個主索引鍵條件約束。 主索引鍵對應到屬性，該屬性會在對應的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 維度中指定為索引鍵屬性。 這個條件約束可以最低的成本，改善大多數環境中的處理效能。 邏輯主索引鍵一律會在資料來源檢視中建立，即使您選擇不在主題領域資料庫中建立主索引鍵也一樣。 若要定義維度資料表上的主索引鍵條件約束，請選取 [在維度資料表上建立主索引鍵]****。  
  
 依預設，精靈也會在每個事實資料表中的外部索引鍵資料行上建立索引。 這些索引會增進大多數環境中的處理效能。 效能之得以增進，是因為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 產生從主題領域資料庫擷取新資料的處理查詢，通常會包含事實資料表和維度資料表之間的許多聯結陳述式。 若要在每個事實資料表中的外部索引鍵資料行上定義索引，請選取 [建立索引]****。  
  
 最後，依預設精靈會在事實資料表和每個維度資料表之間，強制執行參考完整性。 如果您選擇不強制執行參考完整性，結構描述產生精靈還是會在資料庫和資料來源檢視中，建立這些關聯性。 若要強制執行參考完整性，請選取 [強制執行參考完整性]****。  
  
### <a name="preserving-data-for-incremental-generation"></a>保留累加產生的資料  
 重新產生資料庫結構描述時，結構描述產生精靈預設會嘗試保留資料。 如果因為結構描述變更，以致結構描述產生精靈必須刪除任何資料列，則在刪除資料列之前，您會收到警告。 例如，可能因為您卸除維度，或者因為您變更維度屬性時變更了資料類型，所以必須刪除資料列，以解決參考完整性的問題。 若要在重新產生資料庫結構描述時保留資料，請選取 [重新產生時保留資料]****。  
  
## <a name="step-4-specify-naming-conventions"></a>步驟 4：指定命名慣例  
 您可以在精靈的 [指定命名慣例]**** 頁面上，定義 [結構描述產生精靈] 在主題領域資料庫中產生某些物件時，所使用的命名慣例。 如需 [指定命名慣例]**** 頁面上可用選項的詳細資訊，請參閱[指定命名慣例 &#40;結構描述產生精靈&#41; &#40;Analysis Services - 多維度資料&#41;](../specify-naming-conventions-schema-generation-analysis-services-multidimensional-data.md)。  
  
  
