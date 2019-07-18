---
title: 表格式模型 (Analysis Services) 中的翻譯 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ddd49ce6d3edc3f1e2f72a3fe7f5ab61621eef62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162384"
---
# <a name="translations-in-tabular-models-analysis-services"></a>表格式模型 (Analysis Services) 中的翻譯
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 新增翻譯字串支援表格式模型。 模型中的單一物件可具有多個名稱或描述翻譯，因此可在模型定義中支援多語言版本。  
  
 翻譯字串僅適用於諸如 Excel 樞紐分析表清單等用戶端工具中顯示的物件中繼資料 (資料表與資料行的名稱及說明)。  為了使用翻譯字串，用戶端連線會指定文化特性。 在 [Analysis in Excel (Excel 中的分析)]  功能中，您可從下拉式清單選擇語言。 針對其他工具，您可能必須在連接字串中指定文化特性。  
  
 此功能用途並非在於將翻譯的資料載入至模型。 若您想要載入翻譯資料值，則應開發一套處理策略，其中包含擷取自資料提供來源的翻譯字串。  
  
 新增已翻譯中繼資料的一般工作流程如下所示︰  
  
-   產生每個字串翻譯之預留位置的空白轉譯 JSON 檔案  
  
-   將字串翻譯新增至 JSON 檔案  
  
-   將翻譯匯回模型  
  
-   建立、 處理或部署模型  
  
-   使用允許在連接字串中存有 LCID 的用戶端應用程式，連接至模型  
  
## <a name="create-an-empty-translation-file"></a>建立空白轉譯檔案  
 使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 新增翻譯。  
  
1.  按一下 [模型]   > [翻譯]   > [管理翻譯]  。  
  
2.  選取想要提供翻譯的語言，然後按一下 [新增]  。  
  
3.  根據您想要在稍後匯入字串的方式，從清單中選擇一或多個語言。  
  
     翻譯檔案可以包含多種語言，不過若您為每種語言建立一個翻譯檔案，則可使翻譯管理作業更加輕鬆簡易。 您目前建立的翻譯檔案，將會在稍後完整匯入。 若要依語言變更匯入選項，則每種語言皆必須位於其專屬檔案。  
  
4.  按一下 [匯出語言檔案]  。  提供檔案名稱和位置。  
  
 ![ssas-tabular-translate-export](../../analysis-services/tabular-models/media/ssas-tabular-translate-export.png "ssas-tabular-translate-export")  
  
## <a name="add-translations"></a>新增翻譯  
 空白 JSON 轉譯檔案包含特定語言翻譯的中繼資料。 在模型定義末尾的 **Culture** 區段，會指定物件名稱與描述的翻譯預留位置。 您可針對下列項目新增翻譯：  
  
|||  
|-|-|  
|translatedCaption|在支援視覺化呈現表格式模型的所有用戶端應用程式中，會顯示資料表或資料行。|  
|translatedDescription|相較於標題描述並不常見，其在 SSDT 等模型工具中會顯示為模型資訊。|  
  
 不會從檔案刪除任何未指定的中繼資料。  其應與根據的檔案相符。 您僅須新增想要的字串，然後儲存檔案即可。  
  
 雖然看起來可能會近似您應修改的內容，但  **referenceCulture** 區段在模型的預設文化特性中會包含中繼資料。 系統在執行匯入時將不會讀取針對 **referenceCulture** 區段所做的任何變更，且會將其忽略。  
  
 下列範例顯示適用於 **DimProduct** 和 **DimCustomer** 資料表的已翻譯標題及描述。  
  
 ![ssas-tabular-translate-json](../../analysis-services/tabular-models/media/ssas-tabular-translate-json.png "ssas-tabular-translate-json")  
  
> [!TIP]  
>  您可使用任何 JSON 編輯器來開啟檔案，不過建議您使用 Visual Studio 中的 JSON 編輯器，如此一來您亦可在方案總管中使用 [檢視程式碼] 命令，檢視 SSDT 中的表格式模型定義。 若要取得 JSON 編輯器，您必須 [安裝 Visual Studio 2015 完整版](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)。 免費的 Community Edition 包含 JSON 編輯器。  
  
## <a name="import-a-translation-file"></a>匯入翻譯檔案  
 您匯入的翻譯字串會成為模型定義的永久部分。 匯入字串後，即不再參考翻譯檔案。  
  
1.  按一下 [模型]   > [翻譯]   > [匯入翻譯]  。  
  
2.  尋找翻譯檔案，然後按一下 [開啟]  。  
  
3.  或是指定匯入選項。  
  
    |||  
    |-|-|  
    |覆寫現有翻譯|同個語言的全部現有標題或描述，皆會取代為正在匯入的檔案。|  
    |忽略無效的物件|指定應該忽略或標示為錯誤的中繼資料差異。|  
    |將匯入結果寫入至記錄檔|根據預設，記錄檔會儲存至專案資料夾。 匯入完成後，會提供檔案的實際路徑。 記錄檔名稱為 ssdt_translations_log_<\<時間戳記 >。|  
    |匯入前將翻譯備份至 JSON 檔案|備份符合目前所匯入字串文化特性的現有翻譯。  若在模型中未出現匯入的文化特性，則備份將為空白。<br /><br /> 若您稍後需要還原此檔案，可使用此 JSON 檔案取代 model.bim 的內容。|  
  
4.  按一下 **[匯入]** 。  
  
5.  或是您若產生記錄檔或備份，則可在專案資料夾中找到檔案 (例如：C:\Users\Documents\Visual Studio 2015\Projects\Tabular1200-AW\Tabular1200-AW)。  
  
6.  若要確認匯入，請遵循下列步驟：  
  
    -   在方案總管中以滑鼠右鍵按一下 **model.bim** 檔案，然後選擇 [檢視程式碼]  。 按一下 [是]  關閉設計檢視，然後在程式碼檢視中重新開啟 **model.bim**。  如果您安裝完整版的 Visual Studio (例如免費的 Community Edition)，則會在內建的 JSON 編輯器中開啟檔案。  
  
    -   搜尋 **Culture** 或特定翻譯字串，以確認您想要查看的字串確實存在無誤。  
  
## <a name="connect-using-a-locale-identifier"></a>使用地區設定識別碼連接  
 本節說明關於驗證從模型傳回正確字串所用方式的資訊。  
  
1.  在 Excel 中，連接至表格式模型。 此步驟假定模型已部署完成。 若模型僅存在於工作區，請將其部署至 Analysis Services 執行個體以完成驗證檢查。  
  
     或者，您可使用 [在 Excel 中進行分析]  功能來連接至模型  
  
2.  在 [Excel 連接] 對話方塊中，選擇模型中存在的字串翻譯文化特性。 Excel 會偵測模型中定義的文化特性，並據以填入下拉式清單。  
  
     ![ssas-tabular-translations-excel](../../analysis-services/tabular-models/media/ssas-tabular-translations-excel.png "ssas-tabular-translations-excel")  
  
     您建立樞紐分析表時，應會看見已翻譯的資料表與資料行名稱。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services 的全球化案例](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [在 Excel 中進行分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  
