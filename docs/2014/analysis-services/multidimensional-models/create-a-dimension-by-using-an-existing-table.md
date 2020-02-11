---
title: 使用現有的資料表建立維度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], dimensions
- main dimension tables
- dimensions [Analysis Services], standard
- standard dimensions [Analysis Services]
ms.assetid: edd96fbe-1b1c-445a-95d6-7a025e0ee868
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5e65c2b8d543455a168bddc1be5ae5594c2ba8c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66076414"
---
# <a name="create-a-dimension-by-using-an-existing-table"></a>使用現有的資料表建立維度
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，您可以使用中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 [維度 Wizard]，從現有的資料表建立維度。 方法是，選取精靈之 [選取建立方法]**** 頁面的 [使用現有的資料表]**** 選項。 如果您選取此選項，精靈會以維度資料表、其資料行，以及在現有資料來源檢視中之資料行間的任何關聯性為基礎， 並以來源資料表和相關資料表中的資料為範例。 它會使用此資料，定義以維度資料表中資料行為基礎的屬性資料行，並定義屬性的階層 (稱為「使用者定義的」** 階層)。 使用「維度精靈」建立維度之後，您可以使用 [維度設計師] 在維度中加入、移除和設定屬性與階層。  
  
 使用現有的資料表建立維度時，「維度精靈」會引導您進行下列步驟：  
  
-   指定來源資訊  
  
-   選取相關資料表  
  
-   選取維度屬性  
  
-   定義帳戶智慧  
  
> [!NOTE]  
>  如需與本節所述資訊相對應的逐步指示，請參閱 [使用維度精靈建立維度](create-a-dimension-using-the-dimension-wizard.md)。  
  
## <a name="specifying-the-source-information"></a>指定來源資訊  
 您可以在 [指定來源資訊]**** 頁面上，指定來源資訊。 選取包含您要做為維度基礎之資料表的資料來源檢視，開始此程序。 然後，您可以針對您要定義的維度來指定主維度資料表。 主維度資料表是直接連結到事實資料表的資料表。 例如，將 [產品] 資料表指定為 [產品] 維度的主資料表，或為 [員工] 維度指定 [員工] 資料表。 精靈會在資料來源檢視中，自動選取以主索引鍵為基礎的索引鍵資料行。 不過，您可以在適當的時機變更索引鍵資料行。 此索引鍵資料行會決定維度的成員。 例如，您會將 [ProductKey] 定義為 [產品] 維度的索引鍵資料行。  
  
 您可以選擇地定義包含成員名稱的資料行。 依預設，顯示給使用者的成員名稱就是此索引鍵資料行中的值。 索引鍵資料行中的值 (例如，ProductID 或 EmployeeID) 通常是對使用者無意義，且是唯一的、系統產生的索引鍵。 如果您將使用者看到的名稱變更為維度中其他資料行內的對應值，您通常可以提供更有意義的資訊給使用者。 例如，您可以定義包含產品或員工名稱的成員名稱資料行。 如果您變更成員名稱，使用者會看到更詳細描述的名稱，但是查詢仍會使用索引鍵資料行值，以便正確地分辨共用相同名稱的成員。 如果您為索引鍵資料行指定複合索引鍵，您也必須針對索引鍵屬性，指定提供成員值的資料行。 如需如何設定屬性的詳細資訊，請參閱 [維度屬性 (attribute) 屬性 (property) 參考](dimension-attribute-properties-reference.md)。  
  
## <a name="selecting-related-tables"></a>選取相關資料表  
  
> [!NOTE]  
>  如果主維度資料表在資料來源檢視中沒有定義與其他維度資料表之間的任何關聯性，則精靈會略過此步驟。  
  
 如果您要建立雪花維度，您可以在 [選取相關資料表]**** 頁面上，指定其他屬性定義所在的相關資料表。 例如，您要建立想要在其中定義客戶地理位置資料表的客戶維度。 在此情況下，您可以將地理位置資料表定義為相關資料表。  
  
## <a name="selecting-dimension-attributes"></a>選取維度屬性  
 選取維度資料表後，您可以使用 [選取維度屬性]**** 頁面，從這些資料表中選取您要包含在維度中的屬性。 所有這些資料表中的所有基礎資料行都可以當做潛在的維度屬性使用。 您必須選取維度索引鍵屬性，並針對瀏覽啟用。  
  
 根據預設，精靈會將屬性的類型設定為 `Regular`。 不過，您可能想要將特定的屬性對應到更能代表資料的不同屬性類型。 例如， [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] DW 範例資料庫的 dbo.DimAccount 資料表包含可提供帳戶號碼的 AccountCodeAlternateKey 資料行。 您可能想要將此`Regular`屬性對應至`Account Number`類型，而不是將此屬性的類型設定為。  
  
> [!NOTE]  
>  如果建立維度時，尚未設定維度類型和標準屬性類型，請在建立維度後，使用「商業智慧精靈」設定這些值。 如需詳細資訊，請參閱 [將維度智慧加入至維度中](bi-wizard-add-dimension-intelligence-to-a-dimension.md) 或 [將帳戶智慧加入至維度中](bi-wizard-add-account-intelligence-to-a-dimension.md)(適用於帳戶類型維度)。  
  
 精靈會根據指定的屬性類型，自動設定維度類型。 在精靈中指定的屬性類型會針對屬性 (Attribute) 設定 `Type` 屬性 (Property)。 維度及其屬性的 `Type` 屬性設定會提供關於維度內容的資訊給伺服器和用戶端應用程式。 在某些情況下，這些 `Type` 屬性設定只會提供用戶端應用程式的指導，而且是選擇性的。 在其他情況下 (例如 [帳戶]、[時間] 或 [貨幣] 維度)，這些 `Type` 屬性設定會決定特定的伺服器型行為，且在實作某些 Cube 行為時可能會需要用到。  
  
 如需維度和屬性類型的詳細資訊，請參閱 [維度類型](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)、 [設定屬性類型](attribute-properties-configure-attribute-types.md)。  
  
## <a name="defining-account-intelligence"></a>定義帳戶智慧  
  
> [!NOTE]  
>  [維度精靈] 只有在精靈的 [選取維度屬性]**** 頁面上定義了 [帳戶類型]**** 維度屬性時，才會顯示此步驟。  
  
 您可以使用 [定義帳戶智慧]**** 頁面來建立 [帳戶類型] 維度。 如果您要建立 [帳戶類型] 維度，您必須將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所支援的標準帳戶類型對應到維度中帳戶類型屬性的成員。 伺服器會使用這些對應，為各種類型的帳戶資料提供不同的彙總函式和別名。  
  
 若要對應這些帳戶類型，精靈會提供具有下列資料行的資料表：  
  
-   [來源資料表帳戶類型]**** 資料行會列出資料來源資料表中的帳戶類型。  
  
-   [內建帳戶類型]**** 資料行會列出伺服器所支援的對應標準帳戶類型。 如果來源資料使用標準名稱，精靈會將來源類型自動對應到伺服器類型，然後使用此資訊填入 [內建帳戶類型]**** 資料行。 如果伺服器沒有對應帳戶類型，或者您想要變更對應，請從 [內建帳戶類型]**** 資料行的清單中選取不同的類型。  
  
> [!NOTE]  
>  如果在精靈建立 [帳戶] 維度時，尚未對應帳戶類型，請在建立維度後，使用「商業智慧精靈」設定這些對應。 如需詳細資訊，請參閱 [將帳戶智慧加入至維度中](bi-wizard-add-account-intelligence-to-a-dimension.md)。  
  
## <a name="completing-the-wizard"></a>正在完成精靈  
 精靈會掃描維度資料表，以偵測關聯性。 精靈將會在雪花維度中，自動建立索引鍵屬性間的屬性關聯性。  
  
 精靈也會自動偵測維度中是否有父子式關聯性。 當父屬性參考到維度之索引鍵屬性的成員時，父子式關聯性就存在。 此關聯性會定義階層式關聯性，以及維度之分葉成員間的彙總路徑。 如需父子式階層的詳細資訊，請參閱 [父子式階層中的屬性](parent-child-dimension-attributes.md)。  
  
 在 [正在完成精靈]**** 頁面上，輸入新維度的名稱，然後檢閱維度的結構，即可完成精靈。  
  
## <a name="see-also"></a>另請參閱  
 [藉由在資料來源中產生非時間資料表來建立維度](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)   
 [藉由產生時間資料表來建立時間維度](create-a-time-dimension-by-generating-a-time-table.md)   
 [維度屬性屬性參考](dimension-attribute-properties-reference.md)   
 [藉由產生時間資料表來建立時間維度](create-a-time-dimension-by-generating-a-time-table.md)   
 [在資料來源中產生非時間資料表來建立維度](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
