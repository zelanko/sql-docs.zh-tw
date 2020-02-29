---
title: 建立和管理本機資料分割（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- local partitions [Analysis Services]
- partitions [Analysis Services], local
- partitions [Analysis Services], creating
ms.assetid: eaa95278-9ce9-47d5-a6b6-1046e7076599
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c06e40e452fa0db682e2f79b523ddcd90d0450c2
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175787"
---
# <a name="create-and-manage-a-local-partition-analysis-services"></a>建立及管理本機分割區 (Analysis Services)
  您可以建立其他分割區，讓量值群組能夠改善處理效能。 擁有多個分割區可讓您在本機和遠端伺服器上，跨對應數目的實體資料檔案以配置事實資料。 在 Analysis Services 中，分割區可以獨立及平行處理，讓您在伺服器上處理工作負載時，能夠有更強的控制力。

 您可以在模型設計期間，於 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中建立分割區，或是在部署方案之後，使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 XMLA 來建立分割區。 建議您選取一種方法就好。 如果您交替使用這兩種工具，可能會發現，當您後續從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 重新部署方案時，先前在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中對已部署的資料庫所做的變更會被覆寫。

## <a name="before-you-start"></a>開始之前
 檢查您是否有 Business Intelligence 版或 Enterprise 版。 Standard 版不支援多個分割區。 若要[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]檢查版本，請以滑鼠右鍵按一下中的伺服器節點，然後選擇 [**報表** | ]**[一般**]。 如需功能可用性的詳細資訊，請參閱[SQL Server 2014 版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。

 一開始時就務必了解，如果您之後要將分割區合併，則其必須共用相同的彙總設計。 分割區必須要有相同的彙總設計及儲存模式，才能進行合併。

> [!TIP]
>  瀏覽資料來源檢視 (DSV) 中的資料，以了解您要分割之資料的範圍和深度。 例如，如果是依日期進行分割區，則可在日期資料行排序，以決定每個分割區的上限和下限。

## <a name="choose-an-approach"></a>選擇方式
 在建立分割區時，最重要的考量就是要分割資料，以避免重複的資料列。 資料必須儲存在一個且單一的分割區中，以免重複計算任何資料列。 因此，常會依日期進行分割區，這樣您就可以在各分割區之間定義清楚的界限。

 您可以使用下列任一技術，在跨多個分割區間散發事實資料。 下列技術可用來分割資料。

|技巧|建議|
|---------------|---------------------|
|使用 SQL 查詢來分割事實資料|分割區可以來自 SQL 查詢。 在處理期間，SQL 查詢的目的是要擷取資料。 該查詢的 WHERE 子句會針對每個分割區，提供分割資料的篩選。 Analysis Services 會為您產生查詢，但是您必須完整填寫 WHERE 子句，才能正確地分割資料。<br /><br /> 您可以輕易地分割來自單一來源資料表的資料是這個方法的主要優點。 如果所有來源資料皆來自大型事實資料表，您可以建立查詢，將該資料篩選至不同分割區中，而不需要在資料來源檢視 (DSV) 中建立額外的資料結構。<br /><br /> 但有一個缺點，就是使用查詢會中斷分割區與 DSV 之間的繫結。 如果您之後要更新 Analysis Services 專案中的 DSV (例如新增資料行至事實資料表)，則必須手動編輯每個分割區的查詢，以包含新的資料行。 接下來要討論的第二種方法，則沒有這個缺點。|
|使用 DSV 中的資料表以分割事實資料|您可以將分割區繫結至 DSV 中的資料表、具名查詢或檢視。 這三個都是分割區的基礎，且功能皆相同。 整個資料表、具名查詢或檢視會提供所有資料給單一分割區。<br /><br /> 使用資料表、檢視或具名查詢會將所有資料選取邏輯放在 DSV 中，隨著時間會愈來愈容易管理及維護。 這個方法的重要優點是會保留資料表繫結。 如果您之後更新來源資料表，並不需要修改使用它的分割區。 其次，所有資料表，具名查詢和檢視都存在於一個共同的工作空間，這讓更新更為方便，且不需要個別開啟和編輯分割區查詢。|

## <a name="option-1-filter-a-fact-table-for-multiple-partitions"></a>選項 1：篩選多個分割區的事實資料表
 若要建立多個分割區，請於一開始先修改預設分割區的 **Source** 屬性。 根據預設，量值群組是使用繫結至 DSV 中之單一資料表的單一分割區來建立的。 您必須先修改原始分割區，使其只包含一部分的事實資料之後，才能加入更多分割區。 然後您可以繼續建立其他分割區，以儲存資料的其餘部分。

 建構您的篩選，使分割區之間的資料不要重複。 分割區的篩選會指定分割區使用事實資料表中的哪些資料。 在同一個 Cube 中之所有分割區的篩選，都必須從事實資料表擷取互斥的資料集，這點非常重要。 如果相同的事實資料出現在多個分割區中，可能會重複計算。

1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的方案總管中，按兩下 Cube 以在 Cube 設計師中開啟，然後按一下 [分割區]**** 索引標籤。

2.  展開要為其加入分割區的量值群組。 依預設，每個量值群組都有一個分割區會繫結至 DSV 中的事實資料表。

3.  在 Source 資料行中，按一下 [瀏覽] (. .) 按鈕，以開啟 [分割區來源] 對話方塊。

     ![[分割區] 窗格中的來源資料行](../media/ssas-partitionsource.png "[分割區] 窗格中的來源資料行")

4.  在 [繫結類型] 中，選取 [查詢繫結]****。 選取資料的 SQL 查詢會自動出現。

5.  在最下面的 WHERE 子句中，新增為此分割區進行分割資料的篩選。

     WHERE 子句語法的範例包括 `WHERE OrderDateKey >= '20060101'` 或 `WHERE OrderDateKey BETWEEN '20051001' AND '20051201'`。 如需其他範例，請參閱 [WHERE &#40;Transact-SQL&#41;](/sql/t-sql/queries/where-transact-sql)。

     請注意，下列篩選在每一個集合中均為互斥：

    |||
    |-|-|
    |集合 1：|"SaleYear" = 2012<br /><br /> "SaleYear" = 2013|
    |集合 2：|"Continent" = 'NorthAmerica'<br /><br /> "Continent" = 'Europe'<br /><br /> "Continent" = 'SouthAmerica'|
    |集合 3：|"Country" = 'USA'<br /><br /> "Country" = 'Mexico'<br /><br /> ("Country" <> 'USA' AND "Country" <> 'Mexico')|

6.  按一下 [檢查]**** 以檢查語法錯誤，然後按一下 [確定]****。

7.  重複先前的步驟以建立其餘的分割區，並每次修改 WHERE 子句，以選取下一個資料配量。

8.  部署方案或處理分割區以載入資料。 請務必處理所有的分割區。

9. 瀏覽 Cube 以驗證傳回正確的資料。

 在您有了使用多個量值群組的量值群組之後，即可在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中建立其他分割區。 在量值群組底下，以滑鼠右鍵按一下 Partitions 資料夾，並選取 [新增分割區]**** 以啟動精靈。

> [!NOTE]
>  除了在分割區中篩選資料，您可以使用相同的查詢在 DSV 中建立具名查詢，然後以具名查詢做為分割區的基礎。

## <a name="option-2-use-tables-views-or-named-queries"></a>選項 2：使用資料表、檢視或具名查詢
 如果 DSV 已經將事實組織成個別資料表 (例如，依年份或季)，您可以根據個別資料表來建立分割區，而每個分割區都要有自己的資料來源資料表。 基本上，這是分割量值群組的預設方式，但是如果有多個分割區，則要將原始分割區分成多個分割區，並將每個新的分割區對應至提供資料的資料來源資料表。

 檢視和具名查詢的功能相當於資料表，因為這三個物件都定義在 DSV 中，並且是使用 [分割區來源] 對話方塊中的 [資料表繫結] 選項繫結至分割區。 您可以建立檢視或具名查詢以產生每個分割區所需的資料區段。 如需詳細資訊，請參閱[在資料來源檢視中定義具名查詢 &#40;Analysis Services&#41;](define-named-queries-in-a-data-source-view-analysis-services.md)。

> [!IMPORTANT]
>  在 DSV 中建立分割區的互斥具名查詢時，請確定分割區的結合資料，會包含您要在 Cube 中包含之量值群組的所有資料。 請確定您未保留以量值群組之整個資料表為基礎的預設分割區，否則以查詢為基礎的分割區，就會和以整個資料表為基礎的查詢重疊。

1.  建立一個或多個具名查詢，以做為分割區來源。 如需詳細資訊，請參閱[在資料來源檢視中定義具名查詢 &#40;Analysis Services&#41;](define-named-queries-in-a-data-source-view-analysis-services.md)。

     具名查詢必須以與量值群組相關聯的事實資料表為基礎。 例如，若您要分割 FactInternetSales 量值群組，則 DSV 中的具名查詢必須在 FROM 陳述式中指定 FactInternetSales 資料表。

2.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的方案總管中，按兩下 Cube 以在 Cube 設計師中開啟，然後按一下 [分割區]**** 索引標籤。

3.  展開要為其加入分割區的量值群組。

4.  按一下 [新增分割區]****，以啟動 [分割區精靈]。 如果您是使用繫結至量值群組的事實資料表來建立具名查詢，應該就會看到您在前面步驟中建立的每一個具名查詢。

5.  在 [指定來源資訊] 中，選擇您在前面步驟中建立的其中一個具名查詢。 如果沒有看到任何具名查詢，請回到 DSV 並檢查 FROM 陳述式。

6.  按一下 [下一步]**** 以接受每個後續頁面的預設值。

7.  在最後一頁的 [正在完成精靈] 上，提供描述性名稱給分割區。

8.  按一下 [完成]  。

9. 重複先前的步驟以建立其餘的分割區，並每次選擇不同的具名查詢，以選取下一個資料配量。

10. 部署方案或處理分割區以載入資料。 請務必處理所有的分割區。

11. 瀏覽 Cube 以驗證傳回正確的資料。

## <a name="next-step"></a>後續步驟
 建立分割區的互斥查詢時，請確定結合的分割區資料包含您要在 Cube 中包含的所有資料。

 在最後一個步驟中，您通常會想要移除以資料表本身為基礎的預設分割區 (如果還存在的話)，否則以查詢為基礎的分割區會和以完整資料表為基礎的查詢重疊。

## <a name="see-also"></a>另請參閱
 分割區[&#40;Analysis Services 多維度資料&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md) [遠端](../multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)分割區會[在 Analysis Services 中合併分割區 &#40;SSAS-多維度&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)


