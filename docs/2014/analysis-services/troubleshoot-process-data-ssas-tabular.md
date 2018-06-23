---
title: 疑難排解處理資料 (SSAS 表格式) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 678f523c-e181-4456-9a54-7b7bf044b8d2
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8ddebb4bb6a2e1c3e3d4bc53052ff207d7bb1d40
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132274"
---
# <a name="troubleshoot-process-data-ssas-tabular"></a>疑難排解處理資料 (SSAS 表格式)
  本主題提供有關使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]製作模型時，處理 (重新整理) 模型資料的詳細資訊。 本主題不會提供有關處理模型中已部署至 Analysis Services 伺服器執行個體之資料的詳細資訊。 如需在部署的模型中處理資料的詳細資訊，請參閱 [在 Analysis Services 中編寫管理工作的指令碼](script-administrative-tasks-in-analysis-services.md)。  
  
 本主題的章節：  
  
-   [資料處理如何運作](#bkmk_how_df_works)  
  
-   [資料處理的影響](#bkmk_impact_of_df)  
  
-   [判斷資料的來源](#bkmk_det_source)  
  
-   [判斷上次重新整理資料的時間](#bkmk_det_last_ref)  
  
-   [重新整理資料來源的限制](#bkmk_restrictions)  
  
-   [變更資料來源的限制](#bkmk_rest_changes)  
  
##  <a name="bkmk_how_df_works"></a> 資料處理如何運作  
 當您處理資料時，便會以新的資料取代模型設計師中的資料。 您無法只匯入新的資料列或是只變更資料。 模型設計師不會追蹤哪些資料列是在先前加入的。  
  
 資料的處理會以交易的方式進行。 這表示一旦開始更新資料，整個更新不是失敗就是成功，您絕不會擁有部分正確的資料。  
  
 從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]起始的手動資料處理，是由 Analysis Services 的本機記憶體中執行個體所處理。 因此，資料處理作業會影響到電腦上其他工作的效能。 不過，如果您排程使用指令碼在已部署的模型中自動處理資料，Analysis Services 的執行個體便會管理匯入處理及其時機。  
  
##  <a name="bkmk_impact_of_df"></a> 資料處理的影響  
 資料的處理通常會觸發資料的重新計算。  處理資料表示從外部來源取得最新資料；重新計算則表示更新使用已變更資料之所有公式的結果。 處理作業通常會觸發重新計算。  
  
 因此，在您變更資料來源或處理取自資料來源的資料之前，永遠都該注意潛在的影響，並考慮這些潛在的結果：  
  
-   模型資料的某些部分可能會因為資料來源中的變更而中斷。 如果並非所有的資料行都可從資料來源擷取 (例如它們已經遭到刪除或是變更)，處理便會失敗，而您就必須更新在來源資料與模型資料之間的對應。 如需詳細資訊，請參閱[編輯現有的資料來源連接&#40;SSAS 表格式&#41;](edit-an-existing-data-source-connection-ssas-tabular.md)。  
  
-   處理後，某些資料行可能會標示為包含錯誤。 這種錯誤發生的原因，可能是資料行中的 DAX 公式使用當處理時就無法使用的資料、資料行的資料類型變更，或是將無效的值加入外部資料。 若要解決這個問題，您可以編輯公式，或者，如果該公式是以無法再使用的資料為基礎，您可以刪除資料行。  
  
-   使用更新之資料的公式將需要進行重新計算。 視模型的大小而定，這可能會花費一些時間。  
  
-   如果您的模型包含多個資料來源，即使只有一個外部資料來源有變更，您也可能需要處理整個模型 (處理全部)。 例如，如果您建立依賴導出資料行的量值，而且這些導出資料行使用其他導出資料行中的值，模型設計師會先分析相依性，然後依序處理相關物件的整個鏈結。 視相依性的複雜性而定，這可能會花費很長的時間。  
  
-   當您變更篩選時，整個模型都必須進行重新計算。  
  
##  <a name="bkmk_det_source"></a> 判斷資料的來源  
 如果您不確定模型中的資料來自何處，您可以使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的工具來取得詳細資料，其中包括來源檔案名稱和路徑。  
  
#### <a name="to-find-the-source-of-existing-data"></a>尋找現有資料的來源  
  
1.  在模型設計師中，選取包含想要知道其來源之資料的資料表。  
  
2.  按一下 [資料表] 功能表，然後再按一下 [資料表屬性]。  
  
3.  在 [編輯資料表屬性] 對話方塊中，記下針對 [連接名稱] 列出的值。  
  
4.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，按一下 [模型] 功能表上的 [現有連接]。  
  
5.  在 [現有連接] 對話方塊中，選取包含您在步驟 3 找到之名稱的資料來源，然後按一下 [編輯]。  
  
6.  在 [編輯連接] 對話方塊中檢視連接資訊，例如資料庫名稱、檔案路徑或報表路徑。  
  
##  <a name="bkmk_det_last_ref"></a> 判斷上次重新整理資料的時間  
 您可以使用 [資料表屬性] 判斷上次重新整理資料的時間。  
  
#### <a name="to-find-the-date-and-time-that-a-table-was-last-processed"></a>尋找上次處理資料表的日期和時間  
  
1.  在模型設計師中，選取包含想要知道其重新整理日期之資料的資料表。  
  
2.  按一下 **[資料表]** 功能表，然後再按一下 **[資料表屬性]**。  
  
3.  在 [編輯資料表屬性] 對話方塊中，[上次重新整理] 會顯示上次資料表重新整理的日期。  
  
##  <a name="bkmk_restrictions"></a> 重新整理資料來源的限制  
 可從 Analysis Services 執行個體之已部署模型自動處理的資料來源具有一些限制。 請務必只選取符合下列準則的資料來源：  
  
-   資料來源必須在執行資料處理時可使用，並且在指定的位置也可使用。 如果原始資料來源是位於製作模型之使用者的本機磁碟機上，則必須從資料處理作業排除該資料來源，或設法將該資料來源發佈至可透過網路連接存取的位置。 如果您將資料來源移至某個網路位置，請務必在模型設計師中開啟模型，並重複資料擷取步驟。 這是重新建立儲存在資料來源連接屬性的連接資訊所必須執行的動作。  
  
-   您必須使用內嵌在資料來源連接中的認證，來存取資料來源。 當您連接至外部資料來源時，會在資料來源連接中建立內嵌認證。  
  
-   您指定的所有資料來源都必須能夠順利執行資料處理。 否則，這項作業會捨棄處理的資料，並保留模型最後儲存的版本。 請排除任何您不確定的資料來源。  
  
-   資料處理必須不能使模型中的其他資料失效。 當您處理資料子集時，請務必了解一旦較新的資料與不是來自相同時間週期的靜態資料彙總後，模型是否仍然為有效。 身為模型設計師，您必須知道資料的相依性，並確定資料處理是否適用於模型本身。  
  
     外部資料來源是透過您指定的內嵌連接字串、URL 或 UNC 路徑來存取，這些是您在使用 [資料表匯入精靈]，將原始資料匯入模型時所指定。 儲存在資料來源連接中的原始連接資訊，會在後續的資料重新整理作業中重複使用。 不需要為資料處理目的建立和管理不同的連接資訊，只會使用現有的連接資訊。  
  
##  <a name="bkmk_rest_changes"></a> 變更資料來源的限制  
 針對您可以對資料來源所做的變更有一些限制：  
  
-   資料行的資料類型只能變更為相容的資料類型。 例如，如果資料行中的資料包含十進位數字，您無法將資料類型變更為整數。 不過，您可以將數值資料變更為文字。 如需資料類型的詳細資訊，請參閱[支援的資料類型 &#40;SSAS 表格式&#41;](tabular-models/data-types-supported-ssas-tabular.md)。  
  
-   您無法在不同的資料表中複選資料行，並變更這些資料行的內容。 您一次只能使用一個資料表或檢視表。  
  
## <a name="see-also"></a>另請參閱  
 [手動處理資料&#40;SSAS 表格式&#41;](manually-process-data-ssas-tabular.md)   
 [編輯現有的資料來源連接&#40;SSAS 表格式&#41;](edit-an-existing-data-source-connection-ssas-tabular.md)  
  
  