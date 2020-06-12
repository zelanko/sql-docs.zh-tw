---
title: 在資料來源視圖中定義指名的查詢（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- named queries [Analysis Services], creating
- modifying named queries
- data source views [Analysis Services], named queries
ms.assetid: f09ba8aa-950e-4c0d-961e-970de13200be
author: minewiskan
ms.author: owend
ms.openlocfilehash: 243a8ef3c20f21a51f98c38918f8cece4dbf16d6
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546950"
---
# <a name="define-named-queries-in-a-data-source-view-analysis-services"></a>在資料來源檢視中定義具名查詢 (Analysis Services)
  具名查詢是以資料表代表的 SQL 運算式。 在具名查詢中，您可以指定 SQL 運算式，來選取在一個或多個資料來源中的一個或多個資料表所傳回的資料列和資料行。 具名查詢就像資料來源檢視 (DSV) 中具有資料列和關聯性的其他任何資料表一樣，差別在於具名查詢是以運算式為基礎。  
  
 具名查詢可讓您擴充 DSV 中之現有資料表的關聯式結構描述，不需修改基礎資料來源。 例如，一系列具名查詢可以將複雜的維度資料表分割為較小、較簡單的維度資料表，以供資料庫維度使用。 具名查詢也可以用來將一個或多個資料來源中的多個資料庫資料表聯結到單一資料來源檢視資料表中。  
  
## <a name="creating-a-named-query"></a>建立具名查詢  
  
> [!NOTE]  
>  您無法將具名計算加入具名查詢中，也不可以用包含具名計算的資料表做為具名查詢的基礎。  
  
 在建立具名查詢時，您需要指定名稱、傳回資料表的資料行和資料的 SQL 查詢，以及 (選擇性) 具名查詢的描述。 SQL 運算式可以參考資料來源檢視中的其他資料表。 定義具名查詢之後，具名查詢中的 SQL 查詢會傳送至資料來源的提供者，並以整體方式驗證。 如果提供者在 SQL 查詢中找不到任何錯誤，資料行就會加入資料表中。  
  
 SQL 查詢中被參考的資料表和資料行不應該限定，或應該只以資料表名稱來限定。 例如，若要參考資料表中的 SaleAmount 資料行， `SaleAmount` 或 `Sales.SaleAmount` 為有效，但 `dbo.Sales.SaleAmount` 會產生錯誤。  
  
 **注意** ：定義查詢 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 資料來源的具名查詢時，包含相關子查詢與 GROUP BY 子句的具名查詢將會失敗。 如需詳細資訊，請參閱 [知識庫中的](https://support.microsoft.com/kb/274729) Internal Error with SELECT Statement Containing Correlated Subquery and GROUP BY [!INCLUDE[msCoName](../../includes/msconame-md.md)] (包含相互關聯之子查詢和 GROUP BY 的 SELECT 陳述式發生內部錯誤)。  
  
## <a name="add-or-edit-a-named-query"></a>加入或編輯具名查詢  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟含有您想在其中加入具名查詢之資料來源檢視的專案，或連接到包含此資料來源檢視的資料庫。  
  
2.  在方案總管中，展開 [資料來源檢視]**** 資料夾，然後按兩下資料來源檢視。  
  
3.  在 [資料表]**** 或 [圖表]**** 窗格中，以滑鼠右鍵按一下開放區域，然後按一下 [新增具名查詢]****。  
  
4.  在 [建立具名查詢]**** 對話方塊中，執行下列動作：  
  
    1.  在 [名稱]**** 文字方塊中，輸入查詢名稱。  
  
    2.  可以選擇在 [描述]**** 文字方塊中輸入查詢的描述。  
  
    3.  在 [資料來源]**** 清單方塊中，選取具名查詢執行時所要針對的資料來源。  
  
    4.  在下方窗格中輸入查詢，或是使用圖形化查詢建立工具來建立查詢。  
  
    > [!NOTE]  
    >  請注意，建立查詢的使用者介面 (UI) 需視資料來源而定； 您可以取得一般文字式 UI，而非圖形 UI。 您可以使用不同的 UI 來完成相同的工作，但必須以不同的方式執行。 如需詳細資訊，請參閱[建立/編輯具名查詢對話方塊 &#40;Analysis Services - 多維度資料&#41;](../create-or-edit-named-query-dialog-box-analysis-services-multidimensional-data.md)。  
  
5.  按一下 [確定]。 資料表頁首會出現表示兩個重疊資料表的圖示，指出資料表已取代為具名查詢。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源視圖](data-source-views-in-multidimensional-models.md)   
 [在資料來源檢視中定義具名計算 &#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
