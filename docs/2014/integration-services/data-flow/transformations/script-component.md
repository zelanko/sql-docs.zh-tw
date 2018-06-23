---
title: 指令碼元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.scriptcomponentdetails.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
caps.latest.revision: 70
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 56b26f0c43df3257fc563ea246045ad3baf1e3ab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031497"
---
# <a name="script-component"></a>指令碼元件
  指令碼元件可裝載指令碼，並讓封裝包含及執行自訂指令碼。 您可在封裝中使用指令碼元件以達到下列目的：  
  
-   套用多個轉換至資料，而不使用資料流程中的多個轉換。 例如，指令碼可以加總兩個資料行中的值，然後計算總和的平均。  
  
-   存取現有 .NET 組件中的商務規則。 例如，指令碼可以套用商務規則，以指定在 `Income` 資料行中有效的值範圍。  
  
-   除了 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 運算式文法所提供的函數和運算子外，也可以使用自訂公式和函數。 例如，使用 LUHN 公式驗證信用卡號碼。  
  
-   驗證資料行資料並略過包含無效資料的記錄。 例如，指令碼可評估合理的郵資金額，並略過金額過高或過低的記錄。  
  
 指令碼元件提供簡單快速的方式，用來將自訂函數包含在資料流程中。 不過，如果您計劃在多個封裝中重複使用指令碼，應該考慮以程式設計自訂元件，而不要使用指令碼元件。 如需詳細資訊，請參閱 [開發自訂資料流程元件](../../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
> [!NOTE]  
>  如果指令碼元件包含指令碼，而該指令碼嘗試讀取 NULL 的資料行值，則當您執行封裝時，此指令碼元件就會失敗。 我們建議您讓您的指令碼使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.IsNull%2A> 方法來判斷資料行是否為 NULL，然後再嘗試讀取資料行值。  
  
 指令碼元件可當做來源、轉換或目的地使用。 此元件支援一個輸入和多個輸出。 視元件的使用方式而定，可支援輸入、輸出或兩者。 指令碼是由輸入或輸出中的每個資料列所叫用。  
  
-   如果當做來源使用，指令碼元件可支援多個輸出。  
  
-   如果當做轉換使用，指令碼元件可支援一個輸入和多個輸出。  
  
-   如果當做目的地使用，指令碼元件可支援一個輸入。  
  
 指令碼元件不支援錯誤輸出。  
  
 確定指令碼元件是適用於您封裝的選擇之後，您必須設定輸入和輸出、開發該元件使用的指令碼，以及設定元件本身。  
  
## <a name="understanding-the-script-component-modes"></a>了解指令碼元件模式  
 在「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計工具」中，指令碼元件有兩個模式：中繼資料設計模式與程式碼設計模式。 在中繼資料設計模式中，您可以加入和修改指令碼元件輸入和輸出，但是不能編寫程式碼。 設定好所有輸入和輸出後，您可以切換到程式碼設計模式編寫指令碼。 指令碼元件會自動從輸入和輸出的中繼資料產生基底程式碼。 如果您在指令碼元件產生基底程式碼後變更中繼資料，您的程式碼可能無法再編譯，因為更新的基底程式碼可能與您的程式碼不相容。  
  
## <a name="writing-the-script-that-the-component-uses"></a>撰寫元件使用的指令碼  
 指令碼元件使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 當作撰寫指令碼的環境。 您可以從 **[指令碼轉換編輯器]** 存取 VSTA。 如需詳細資訊，請參閱 [指令碼轉換編輯器 &#40;指令碼頁面&#41;](../../script-transformation-editor-script-page.md)。  
  
 指令碼元件提供 VSTA 專案，其中包含自動產生的類別，該類別名為 ScriptMain 且代表元件中繼資料。 例如，如果指令碼元件當做具有三個輸出的轉換使用，則 ScriptMain 會包含每個輸出的方法。 ScriptMain 是指令碼的進入點。  
  
 VSTA 包含 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 環境的所有標準功能，例如色彩編碼的 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 編輯器、IntelliSense 和「物件瀏覽器」。 指令碼元件所使用的指令碼會儲存在封裝定義中， 當您要設計封裝時，指令碼會暫時寫入專案檔。  
  
 VSTA 支援 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 程式語言。  
  
 如需有關如何以程式設計方式編寫指令碼元件的詳細資訊，請參閱＜ [以指令碼元件來擴充資料流程](script-component.md)＞。 如需有關如何將指令碼元件設為來源、轉換或目的地的特定資訊，請參閱＜ [Developing Specific Types of Script Components](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)＞。 如需其他範例 (例如示範如何使用指令碼元件的 ODBC 目的地)，請參閱＜ [Additional Script Component Examples](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)＞。  
  
> [!NOTE]  
>  不像在舊版中可以指出是否已經先行編譯指令碼，所有指令碼在 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 和更新的版本中都會先行編譯。 指令碼經過先行編譯後，在執行階段不會載入語言引擎，因此封裝的執行速度會更快。 不過，先行編譯的二進位檔案會使用大量的磁碟空間。  
  
## <a name="configuring-the-script-component"></a>設定指令碼元件  
 您可以利用下列方式設定指令碼元件：  
  
-   選取要參考的輸入資料行。  
  
    > [!NOTE]  
    >  當您使用「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計工具」時，僅能設定一個輸入。  
  
-   提供元件執行的指令碼。  
  
-   指定指令碼語言。  
  
-   提供唯讀和讀取/寫入變數的逗號分隔清單。  
  
-   加入更多輸出，並加入指令碼指派的目標輸出資料行。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
### <a name="configuring-the-script-component-in-the-designer"></a>在設計工具中設定指令碼元件  
 如需有關可以在 **[指令碼轉換編輯器]** 對話方塊中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [指令碼轉換編輯器&#40;輸入資料行頁面&#41;](../../script-transformation-editor-input-columns-page.md)  
  
-   [指令碼轉換編輯器&#40;輸入及輸出頁面&#41;](../../script-transformation-editor-inputs-and-outputs-page.md)  
  
-   [指令碼轉換編輯器&#40;指令碼 頁面&#41;](../../script-transformation-editor-script-page.md)  
  
-   [指令碼轉換編輯器&#40;連接管理員頁面&#41;](../../script-transformation-editor-connection-managers-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>以程式設計的方式設定指令碼元件  
 如需有關可以在 **[屬性]** 視窗中或以程式設計的方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相關內容  
 [Integration Services 轉換](integration-services-transformations.md)  
  
 [以指令碼元件來擴充資料流程](script-component.md)  
  
  