---
title: 多維度模型 (Analysis Services) 中的翻譯 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5d5d209558246f9d2d33113f81199bd2ee1ca66a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="translations-in-multidimensional-models-analysis-services"></a>多維度模型中的翻譯 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中定義翻譯，方法是針對要翻譯的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件使用適當的設計師。 定義翻譯會建立 **Translation** 物件，並與適當的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件相關聯，其中會以指定的語言和指定的明確常值，來設定相關聯之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的屬性。  
  
## <a name="elements-of-a-multi-lingual-data-model"></a>多語言資料模型的元素  
 多語系方案中所使用的資料模型不只需要翻譯的標籤 (欄位名稱和描述)， 也必須提供以各種字集表示的資料值。 您必須具有繫結至外部資料庫中資料行並傳回資料的個別屬性，才能取得多語系方案。  
  
 Adventure Works 範例資料庫 (多維度及關聯式資料倉儲) 示範 Analysis Services 的翻譯功能。 範例模型包含翻譯的標題和描述。 範例關聯式資料倉儲包含多欄翻譯值，這些值提供模型中的當地語系化屬性成員。  
  
 若要檢視模型可用的翻譯資料值：  
  
1.  在設計工具中，開啟 Adventure Works 多維度模型。  
  
2.  在 [方案總管] 中，開啟資料來源檢視，然後按兩下 Adventure Works DW\<版本 >.dsv。  
  
3.  尋找 dimDate、dimProduct、dimProductCategory 或 dimProductSubcateogry。 上述所有維度包含月、週中的日、產品名稱、類別目錄名稱等翻譯成員的屬性。  
  
4.  以滑鼠右鍵按一下任何欄位，然後選取 [瀏覽資料] 。 您會看到每個成員的英文、西班牙文和法文翻譯。  
  
 日期、時間和貨幣格式的實作未透過翻譯。 若要根據用戶端的地區設定，以動態方式提供特定文化特性的格式，請使用 [貨幣轉換精靈] 和 **FormatString** 屬性。 如需詳細資訊，請參閱[貨幣轉換 &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md) 和 [FormatString 元素 &#40;ASSL&#41;](../../analysis-services/scripting/properties/formatstring-element-assl.md)。  
  
 Analysis Services 教學課程中的[Lesson 9: Defining Perspectives and Translations](../../analysis-services/lesson-9-defining-perspectives-and-translations.md) 將逐步引導您完成建立及測試翻譯的步驟。  
  
## <a name="defining-translations"></a>定義翻譯  
  
### <a name="add-translations-to-a-cube"></a>將翻譯加入 Cube  
 您可以將翻譯加入 Cube、量值群組、量值、Cube 維度、檢視方塊、KPI、動作、命名集和導出成員。  
  
1.  在 [方案總管] 中，按兩下 Cube 名稱，開啟 Cube 設計師。  
  
2.  按一下 **[翻譯]** 索引標籤。支援翻譯的所有物件會列在這個頁面中。  
  
3.  針對每個物件，指定目標語言 (內部解析成 LCID)、翻譯的標題和翻譯的描述。 不論您要在 Management Studio 中設定伺服器語言，或在單一屬性上加入翻譯覆寫，語言清單在整個 Analysis Services 中都是一致的。  
  
     請記住，您無法變更定序。 Cube 基本上會使用一個定序，即使您正在透過翻譯的標題支援多個語言亦然 (維度屬性除外，下面將提供說明)。 如果語言未依共用的定序正確排序，您將需要複製 Cube，以符合您的定序需求。  
  
4.  建立及部署專案。  
  
5.  使用用戶端應用程式 (例如 Excel) 連接至資料庫，並修改連接字串以使用地區設定識別碼。 如需詳細資訊，請參閱[全球化秘訣和最佳作法 &#40;Analysis Services&#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md)。  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>將翻譯加入維度和屬性  
 您可以將翻譯加入資料庫維度、屬性、階層和階層內的層級。  
  
 您可以使用鍵盤或複製-貼上作業將翻譯的標題手動加入模型；至於維度屬性成員，則可以從外部資料庫取得翻譯值。 具體來說，屬性 (Attribute) 的 **CaptionColumn** 屬性 (Property) 可繫結至資料來源檢視中的資料行。  
  
 在屬性層級，您可以覆寫定序設定，例如您可能想要針對特定屬性調整區分全半形或使用二進位排序。 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，會公開已定義資料繫結的定序。 由於您要將維度屬性翻譯繫結至 DSV 中的不同來源資料行，因此您可以使用定序設定，來指定來源資料行所使用的定序。 如需關聯式資料庫中資料行定序的詳細資訊，請參閱 [Set or Change the Column Collation](../../relational-databases/collations/set-or-change-the-column-collation.md) 。  
  
1.  在 [方案總管] 中，按兩下維度名稱，開啟維度設計師。  
  
2.  按一下 **[翻譯]** 索引標籤。支援翻譯的所有維度物件會列在這個頁面中。  
  
     針對每個物件，指定目標語言 (解析成 LCID)、翻譯的標題和翻譯的描述。 不論您要在 Management Studio 中設定伺服器語言，或在單一屬性上加入翻譯覆寫，語言清單在整個 Analysis Services 中都是一致的。  
  
3.  若要將屬性繫結至提供翻譯值的資料行：  
  
    1.  在維度設計師 | [翻譯] 中，加入新翻譯。 選擇語言。 接受翻譯值的新資料行隨即出現在頁面上。  
  
    2.  將游標置於與其中一個屬性相鄰的空資料格中。 屬性不可以是索引鍵，但其他所有屬性都是可用選項。 您應該會看到中間有個點的小按鈕。 按一下按鈕，開啟 [屬性資料翻譯] 對話方塊。  
  
    3.  輸入標題的翻譯。 這會做為目標語言的資料標籤，例如樞紐分析表欄位清單中的欄位名稱。  
  
    4.  選擇提供屬性成員之翻譯值的來源資料行。 只能使用繫結至維度之資料表或查詢中已存在的資料行。 如果該資料行不存在，您需要修改資料來源檢視、維度和 Cube，以取得資料行。  
  
    5.  選擇定序和排序順序 (如果適用的話)。  
  
4.  建立及部署專案。  
  
5.  使用用戶端應用程式 (例如 Excel) 連接至資料庫，並修改連接字串以使用地區設定識別碼。 如需詳細資訊，請參閱[全球化秘訣和最佳作法 &#40;Analysis Services&#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md)。  
  
### <a name="add-a-translation-of-the-database-name"></a>加入資料庫名稱的翻譯  
 在資料庫層級，您可以加入資料庫名稱和描述的翻譯。 您可能會在指定語言 LCID 的用戶端連接上看到翻譯的資料庫名稱，但這會視工具而定。 例如，即使您指定連接上的地區設定識別碼，在 Management Studio 中檢視資料庫也不會顯示翻譯的名稱。 Management Studio 用來連接至 Analysis Services 的 API 不會讀取 **Language** 屬性。  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下專案名稱 | [編輯資料庫]  ，開啟資料庫設計工具。  
  
2.  在 [翻譯] 中，指定目標語言 (解析成 LCID)、翻譯的標題和翻譯的描述。 不論您要在 Management Studio 中設定伺服器語言，或在單一屬性上加入翻譯覆寫，語言清單在整個 Analysis Services 中都是一致的。  
  
3.  在資料庫的 [屬性] 頁面中，將 **Language** 設為您為翻譯所指定的相同 LCID。 選擇性地另外設定 **Collation** (如果預設值不再適用)。  
  
4.  建立及部署資料庫。  
  
## <a name="deleting-translation-objects"></a>刪除翻譯物件  
 您可以用滑鼠右鍵按一下維度或 Cube 設計師中的翻譯物件，永久將它移除。 由於您無法還原或回收刪除的物件，因此務必要在繼續進行之前檢閱受影響物件的清單。  
  
## <a name="resolving-translations"></a>解析翻譯  
 如果用戶端應用程式要求指定之語言識別碼中的資訊， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會嘗試將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的資料和中繼資料解析成最接近的語言識別碼。 如果用戶端應用程式未指定預設語言，或指定中性地區設定識別碼 (0) 或處理序預設語言識別碼 (1024)，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用執行個體的預設語言來傳回 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的資料和中繼資料。  
  
 如果用戶端應用程式指定的語言識別碼不是預設語言識別碼，則執行個體會對所有可用的物件逐一查看所有可用的翻譯。 如果指定的語言識別碼符合翻譯的語言識別碼， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會傳回該翻譯。 如果找不到相符項目， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會嘗試使用下列其中一個方法，來傳回具有最接近指定之語言識別碼的翻譯：  
  
-   針對下列語言識別碼，如果尚未定義指定之語言識別碼的翻譯，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會嘗試使用替代語言識別碼：  
  
    |指定的語言識別碼|替代語言識別碼|  
    |-----------------------------------|-----------------------------------|  
    |3076 - 中文 (中國香港特別行政區)|1028 - 中文 (台灣)|  
    |5124 - 中文 (澳門特別行政區)|1028 - 中文 (台灣)|  
    |1028 - 中文 (台灣)|預設語言|  
    |4100 - 中文 (新加坡)|2052 - 中文 (中華人民共和國)|  
    |2074 - 克羅埃西亞文|預設語言|  
    |3098 - 克羅埃西亞文 (斯拉夫文)|預設語言|  
  
-   針對所有其他指定的語言識別碼， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會擷取 (extract) 所指定之語言識別碼的主要語言，並擷取 (retrieve) Windows 所指出的語言識別碼作為主要語言的最符合項目。 如果找不到最符合之語言識別碼的翻譯，或指定的語言識別碼是主要語言的最符合項目，則使用預設語言。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的全球化案例](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [語言和定序&#40;Analysis Services&#41;](../../analysis-services/languages-and-collations-analysis-services.md)  
  
  
