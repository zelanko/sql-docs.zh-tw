---
title: "授與對維度資料 (Analysis Services) 的自訂存取權 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.roledesignerdialog.dimensiondata.f1
helpviewer_keywords:
- dimensions [Analysis Services], security
- AllowedSet property
- IsAllowed property
- DeniedSet property
- user access rights [Analysis Services], dimensions
- custom dimension data access [Analysis Services]
- permissions [Analysis Services], dimensions
- DefaultMember property
- VisualTotals property
- ApplyDenied property
ms.assetid: b028720d-3785-4381-9572-157d13ec4291
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 42ea70f08c2f051970898fa4e3e9498f7f8c1627
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="grant-custom-access-to-dimension-data-analysis-services"></a>授與維度資料的自訂存取權 (Analysis Services)
  啟用 Cube 的讀取權限後，您可以設定額外的權限以明確允許或拒絕維度成員 (包括 Measures 維度中的量值，其中含有 Cube 中使用的所有量值) 的存取。 例如，假設指定了多個轉售商類別，您可能想要設定權限以排除特定商業類型的資料。 下圖為拒絕存取 Reseller 維度中之 Warehouse 商業類型之前與之後的效果。  
  
 ![不具有維度成員與樞紐分析表](../../analysis-services/multidimensional-models/media/ssas-permsdimdenied.png "不具有維度成員與樞紐分析表")  
  
 根據預設，如果您可以從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube 讀取資料，則會自動取得與 Cube 相關聯之所有量值和維度成員的讀取權限。 儘管這個行為對於許多案例可能已經足夠，但有時安全性需求會針對相同維度上的不同使用者來變動存取層級，藉以要求更多區段的授權策略。  
  
 您可以藉由選擇要允許 (AllowedSet) 或拒絕 (DeniedSet) 哪些成員存取，來限制存取權。 您可以選取或取消選取要在角色中包含或排除的維度成員，來完成這個動作。  
  
 基本維度安全性是最簡單的；您只需選取要在角色中包含或排除的維度屬性和屬性階層。 進階安全性較複雜，而且需要 MDX 指令碼的專業知識。 以下是這兩種方法的敘述。  

> [!NOTE]  
>  下列指示假設用戶端連接使用 MDX 發出查詢。 如果用戶端使用 DAX (例如 Power BI 中的 Power View)，則查詢結果中不會顯示維度安全性。 如需詳細資訊，請參閱[了解適用於多維度模型的 Power View](understanding-power-view-for-multidimensional-models.md)。
      
## <a name="prerequisites"></a>必要條件  
 並非所有量值或維度成員均可用在自訂存取案例中。 如果某個角色禁止存取預設的量值或成員，或是該角色禁止存取的量值為量值運算式的一部分，則連線將會失敗。  
  
 **檢查維度安全性的限制：預設量值、預設成員及量值運算式中使用的量值**  
  
1.  在 SQL Server Management Studio，以滑鼠右鍵按一下 cube，然後選取**指令碼的 Cube 做** | **ALTER 至** | **新增查詢編輯器視窗**。  
  
2.  搜尋 **DefaultMeasure**。 您應該會在 Cube 中發現一個，在每個檢視方塊中各發現一個。 當您定義維度安全性時，請避免限制對預設量值的存取。  
  
3.  接下來，搜尋 **MeasureExpression**。 量值運算式是依據某項計算的量值，而計算通常還包含其他量值。 確認您要限制的量值並未使用於運算式中。 或者，當您限制存取的同時，務必也在整個 Cube 中一併排除對該量值的所有參考。  
  
4.  最後，搜尋 **DefaultMember**。 記下做為屬性預設成員的所有屬性。 設定維度安全性時，請避免對那些屬性設定限制。  
  
## <a name="basic-dimension-security"></a>基本維度安全性  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，在物件總管中展開適當資料庫的 [角色]，然後按一下資料庫角色 (或建立新的資料庫角色)。  
  
     角色應該已具備 Cube 的讀取權限。 如果您需要這個步驟的說明，請參閱[授與 Cube 或模型權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)。  
  
2.  在 [維度資料] | [基本] 上，選取您正在設定權限的維度。  
  
3.  選擇屬性階層。 並非所有屬性都是可用的。 只有擁有 [AttributeHierarchyEnabled] 的屬性會出現在 [屬性階層] 清單中。  
  
4.  選擇要允許或拒絕存取的成員。 預設會透過 [選取全部成員] 選項來允許存取。 建議您保留這個預設值，然後清除不應透過這個角色讓 [成員資格] 窗格中的 Windows 使用者和群組帳戶看見的個別成員。 這麼做的好處在於以這個角色連線的使用者，都能夠使用後續處理作業中新增的成員。  
  
     或者，您可以 [取消選取全部成員] 來全面撤銷存取，然後挑選要允許的成員。 在後續的處理作業中，一直到您手動編輯維度資料安全性來允許存取新成員為止，將無法看到任何新成員。  
  
5.  選擇性地按一下 [進階] 以針對這個屬性階層啟用 [視覺化總計]。 這個選項會根據可透過這個角色使用的成員，重新計算彙總。  
  
    > [!NOTE]  
    >  在套用變更維度成員的權限時，並不會自動重新計算彙總的總計。 假設在套用權限之前，屬性階層的 [全部] 成員數目是傳回 200 個。 在將拒絕存取的權限套用到部分成員之後，[全部] 仍會傳回 200，即使使用者可看見的成員值比較少也一樣。 為了避免與您 Cube 的取用者相混淆，您可以設定 [全部] 成員只等於角色成員中之成員的彙總，而不是屬性階層所有成員的彙總。 若要叫用這個行為，您可以在設定維度安全性時，於 [進階] 索引標籤上啟用 [視覺化總計]。 啟用之後，彙總會在查詢期間計算，而不是從預先計算的彙總中擷取。 這可以在查詢效能上產生顯著效果，因此只有在需要時才使用它。  
  
## <a name="hiding-measures"></a>隱藏量值  
 在 [授與資料格資料的自訂存取權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)中，已說明如要完全隱藏量值的所有可見層面 (而非只是它的資料格資料)，需具備維度成員的權限。 本節說明如何拒絕存取量值的物件中繼資料。  
  
1.  在**維度資料** | **基本**，向下的捲動直到您到達 cube 維度，然後選取維度清單**Measures 維度**。  
  
2.  從量值清單中，清除透過這個角色連接的使用者不應看見之量值的核取方塊。  
  
> [!NOTE]  
>  查看 [必要條件] 以了解如何識別可能破壞角色安全性的量值。  
  
## <a name="advanced-dimension-security"></a>進階維度安全性  
 如果您精通 MDX，另一個方法是撰寫 MDX 運算式來設定條件以允許或拒絕成員的存取。 按一下 [建立角色] | [維度資料] | [進階]，以提供指令碼。  
  
 您可以使用 MDX 產生器來撰寫 MDX 陳述式。 如需詳細資訊，請參閱 [MDX 產生器 &#40;Analysis Services - 多維度資料&#41;](http://msdn.microsoft.com/library/fecbf093-65ea-4e1b-b637-f04876f1cb0f)。 [進階] 索引標籤具有下列選項：  
  
 **Attribute**  
 選取您要管理其成員安全性的屬性。  
  
 **允許的成員集**  
 AllowedSet 可以解析為沒有成員 (預設值)、全部成員或部分成員。 如果您允許屬性的存取，但未定義允許集合的成員，就會授與所有成員的存取權。 如果您允許對屬性的存取，而且有定義一組特定的屬性成員，則只有明確允許的成員會是可見的。  
  
 建立 AllowedSet，會在屬性參與多層級階層時產生漣漪效果。 例如，假設有一個角色允許存取 Washington 州 (假設已將公司的 Washington 州業務部門權限授與角色)。 對於透過這個角色連接的人員，包含上階 (United States) 或下階 (Seattle 和 Redmond) 的查詢將只會看見包含 Washington 州之鏈結中的成員。 因為並未明確允許其他州，所以效果會和拒絕它們一樣。  
  
> [!NOTE]  
>  如果您定義空的屬性成員集合 ({})，資料庫角色就看不到該屬性的任何成員。 沒有允許的集合不會被解釋為空的集合。  
  
 **拒絕的成員集**  
 DeniedSet 屬性可以解析為沒有成員、全部成員 (預設值) 或部分屬性成員。 當拒絕的集合僅包含特定的屬性成員集合時，資料庫角色只會被拒絕存取這些特定成員以及下階 (如果屬性位於多層級階層中)。 請考量 Washington 州業務部門範例。 如果將 Washington 放在 DeniedSet 中，透過這個角色連接的人員將看見除了 Washington 及其下階屬性以外的所有其他州。  
  
 一如前文所述，拒絕的集合是固定的集合。 如果後續處理引進了也應該拒絕存取的新成員，您就需要編輯這個角色，來將這些成員新增到清單中。  
  
 **預設成員**  
 若屬性 (Attribute) 未明確包含在查詢中，則會由 DefaultMember 屬性 (Property) 決定要傳回至用戶端的資料集。 未明確包含屬性時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會對該屬性使用下列其中一個預設成員：  
  
-   如果資料庫角色有定義屬性的預設成員， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會使用此預設成員。  
  
-   如果資料庫角色沒有定義屬性的預設成員， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會使用該屬性本身定義的預設成員。 除非您另外指定，否則屬性的預設成員就是 **All** 成員 (除非該屬性定義為非彙總)。  
  
 例如，假設資料庫角色指定 **Male** 作為 **Gender** 屬性的預設成員。 除非查詢明確包含 **Gender** 屬性並為此屬性指定不同成員，否則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會傳回只包含男性客戶的資料集。 如需設定預設成員的詳細資訊，請參閱 [定義預設成員](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)。  
  
 **啟用視覺化總計**  
 VisualTotals 屬性會指出所顯示彙總資料格的值，是根據所有資料格值來計算，還是只根據資料庫角色所看見資料格的值來計算。  
  
 依預設，會停用 VisualTotals 屬性 (設定為 **False**)。 此預設值會使效能最佳化，因為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可快速計算所有資料格的值之總計，而不必浪費時間選取要計算之資料格的值。  
  
 不過，停用 VisualTotals 屬性會產生安全性問題，因為使用者有可能使用彙總資料格的值來推論該使用者的資料庫角色沒有存取權之屬性成員的值。 例如， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用三個屬性成員的值來計算彙總資料格的值。 資料庫角色有檢視這三個屬性成員當中兩個的存取權。 利用彙總資料格的值，此資料庫角色的成員即可推論出第三個屬性成員的值。  
  
 將 VisualTotals 屬性設定為 **True** 可減少這項風險。 當您啟用 VisualTotals 屬性時，資料庫角色只能檢視該角色具有權限之維度成員的彙總。  
  
 **檢查**  
 按一下即可測試此頁面定義的 MDX 語法。  
  
## <a name="see-also"></a>另請參閱  
 [授與 Cube 或模型權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [授與自訂資料 &#40; 的儲存格的存取Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)   
 [授與權限的資料採礦結構和模型 &#40;Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [授與資料來源物件的權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  

