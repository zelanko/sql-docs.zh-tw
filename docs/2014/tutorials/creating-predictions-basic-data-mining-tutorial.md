---
title: 建立預測 （基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a8410ed2-bb98-4d51-a9eb-b239be1201c2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3940f7c214ab3f9d5d48e83acef5ed2237ceeac3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206528"
---
# <a name="creating-predictions-basic-data-mining-tutorial"></a>建立預測 (基本資料採礦教學課程)
  您已測試好採礦模型的精確度，並決定您滿意結果之後，您可以上使用預測查詢產生器，然後產生預測**採礦模型預測**在資料採礦 索引標籤設計工具。  
  
 預測查詢產生器有三個檢視。 具有**設計**並**查詢**檢視，您可以建置並檢查您的查詢。 您可以再執行查詢，並檢視中的結果**結果**檢視。  
  
 所有的預測查詢都是使用 DMX，也就是資料採礦延伸模組 (DMX) 語言的縮寫。 DMX 的語法與 T-SQL 的語法相似，但用於對資料採礦物件的查詢。 雖然 DMX 語法並不複雜，但是使用這類工具或查詢產生器[SQL Server Data Mining Add-ins for Office](../../2014/analysis-services/data-mining/sql-server-data-mining-add-ins-for-office.md)，更輕鬆地選取輸入和建立運算式，因此強烈建議您深入了解基本概念。  
  
## <a name="creating-the-query"></a>建立查詢  
 建立預測查詢的第一個步驟是，選取採礦模型和輸入資料表。  
  
#### <a name="to-select-a-model-and-input-table"></a>若要選取模型和輸入資料表  
  
1.  在上**採礦模型預測**] 索引標籤的 [資料採礦設計師中**採礦模型**方塊中，按一下**選取模型**。  
  
2.  在**選取採礦模型**對話方塊方塊中，瀏覽樹狀目錄以**Targeted Mailing**結構中，展開結構，並選取`TM_Decision_Tree`，然後按一下  **確定**.  
  
3.  在 **選取輸入資料表**方塊中，按一下**選取案例資料表**。  
  
4.  在 **選取表格**對話方塊中，於**資料來源**清單中，選取資料來源檢視[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]。  
  
5.  在 **資料表/檢視名稱**，選取**ProspectiveBuyer (dbo)** 資料表，然後按一下 **確定**。  
  
     `ProspectiveBuyer`資料表最接近**vTargetMail**案例資料表。  
  
## <a name="mapping-the-columns"></a>對應資料行  
 選好輸入資料表之後，「預測查詢產生器」會根據資料行的名稱，在採礦模型和輸入資料表之間建立預設的對應。 此結構中至少必須有一個資料行符合外部資料中的資料行。  
  
> [!IMPORTANT]  
>  您用來判斷模型精確度的資料必須包含可對應至可預測資料行的資料行。 如果這類資料行不存在，您可以建立包含空值的資料行，但是其資料類型必須與預測的資料行相同。  
  
#### <a name="to-map-the-inputs-to-the-model"></a>將輸入對應至模型  
  
1.  以滑鼠右鍵按一下連接的線條**採礦模型** 視窗來**選取輸入資料表**視窗中，然後選取**修改連接**。  
  
     請注意，並非每一個資料行都會對應。 我們會將對應加入數個**資料表資料行**。 另外還會依據目前的日期資料行產生新的生日資料行，讓資料行更好比對。  
  
2.  底下**資料表資料行**，按一下 `Bike Buyer`資料格，然後從下拉式清單中選取 ProspectiveBuyer.Unknown。  
  
     這會將可預測的資料行 [Bike Buyer] 對應到輸入資料表資料行。  
  
3.  按一下 [確定] 。  
  
4.  在 [**方案總管] 中**，以滑鼠右鍵按一下**Targeted Mailing**資料來源檢視，並選取**檢視表設計工具**。  
  
5.  以滑鼠右鍵按一下資料表，也就是 ProspectiveBuyer，然後選取**新增具名計算**。  
  
6.  在 [**建立具名計算**] 對話方塊中，如**資料行名稱**，型別`calcAge`。  
  
7.  針對**描述**，型別**計算的出生日期所根據的年齡**。  
  
8.  在 **運算式**方塊中，輸入`DATEDIFF(YYYY,[BirthDate],getdate())`，然後按一下**確定**。  
  
     由於輸入的資料表沒有**年齡**資料行對應至在模型中，您可以使用此運算式來計算客戶的年齡，從輸入資料表的 BirthDate 資料行。 由於**年齡**已被識別為最具影響力資料行來預測自行車購買行為，它必須存在於這兩個模型和輸入資料表。  
  
9. 在 資料採礦設計師中，選取**採礦模型預測**索引標籤，然後重新開啟**修改連接**視窗。  
  
10. 底下**資料表資料行**，按一下**年齡**資料格，然後從下拉式清單中選取 ProspectiveBuyer.calcAge。  
  
    > [!WARNING]  
    >  如果您未在清單中看見資料行，可能必須重新整理設計師中所載入資料來源檢視的定義。 若要這樣做，請從**檔案**功能表上，選取**全部儲存**，然後關閉再重新開啟設計工具中的專案。  
  
11. 按一下 [確定] 。  
  
## <a name="designing-the-prediction-query"></a>設計預測查詢  
  
1.  第一個按鈕的工具列上**採礦模型預測**索引標籤**切換到設計檢視 / 切換到結果檢視 / 切換到查詢檢視** 按鈕。 按一下此按鈕時，向下的箭頭，然後選取**設計**。  
  
2.  在上方格**採礦模型預測**索引標籤上，按一下中的第一個空白資料列的資料格**來源**資料行，然後選取**預測函數**。  
  
3.  在 **預測函數**資料列中**欄位**欄中，選取`PredictProbability`。  
  
     在 **別名**相同的資料列型別資料行**結果機率**。  
  
4.  從**採礦模型**視窗中，選取，然後將 [Bike Buyer] 拖曳至**準則/引數**資料格。  
  
     當您放開滑鼠，[TM_Decision_Tree]。[Bike Buyer] 就會出現在**準則/引數**資料格。  
  
     這會指定 `PredictProbability` 函數的目的地資料行。 如需函式的詳細資訊，請參閱[資料採礦延伸模組&#40;DMX&#41;函式參考](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
5.  按一下 下一步中的空白資料列**來源**資料行，並接著選取 TM_Decision_Tree 採礦模型 **。**  
  
6.  在 `TM_Decision_Tree`資料列中**欄位**欄中，選取`Bike Buyer`。  
  
7.  在 `TM_Decision_Tree`資料列中**準則/引數**資料行中輸入`=1`。  
  
8.  按一下 下一步中的空白資料列**來源**資料行，然後選取**ProspectiveBuyer 資料表**。  
  
9. 在 `ProspectiveBuyer`資料列中**欄位**欄中，選取**prospectivebuyerkey**。  
  
     這會在預測查詢中加入唯一識別碼，供您辨識可能會購買和可能不會購買自行車的人。  
  
10. 將其他五個資料列加入至方格中。 針對每個資料列中，選取**ProspectiveBuyer 資料表**作為**來源**然後新增下列中的資料行**欄位**資料格：  
  
    -   calcAge  
  
    -   LastName  
  
    -   FirstName  
  
    -   AddressLine1  
  
    -   AddressLine2  
  
 最後，執行此查詢並瀏覽結果。  
  
 **預測查詢產生器**也包含下列控制項：  
  
-   **顯示**核取方塊  
  
     讓您可以移除查詢中的子句，而不必從設計師將其刪除。 當您使用複雜的查詢而想要保留語法時，這樣就不必複製 DMX 再貼入視窗，所以相當實用。  
  
-   **群組**  
  
     在所選該行的開頭插入左括號，或在目前該行的結尾插入右括號。  
  
-   **和 （或)**  
  
     在目前的函數或資料行的正後方插入 `AND` 運算子或 `OR` 運算子。  
  
#### <a name="to-run-the-query-and-view-results"></a>若要執行查詢並檢視結果  
  
1.  在 [**採礦模型預測**索引標籤上，選取**結果**] 按鈕。  
  
2.  當執行此查詢並顯示結果之後，您可以檢閱結果。  
  
     **採礦模型預測**索引標籤會顯示有可能購買自行車的潛在客戶的連絡資訊。 **結果的機率**資料行會指出預測正確的機率。 您可以利用這些結果來判斷哪些潛在的客戶應該成為郵寄目標。  
  
3.  此時，您可以儲存結果。 您有三個選項：  
  
    -   以滑鼠右鍵按一下結果中的資料列，然後選取**複製**，將只該值 （和資料行標題） 儲存至剪貼簿。  
  
    -   以滑鼠右鍵按一下任何資料列在結果中，然後選取**全部複製**複製整個結果集，包括資料行標題，到剪貼簿。  
  
    -   按一下 **儲存查詢結果**將結果直接與資料庫，如下所示：  
  
        1.  在 [**儲存資料採礦查詢結果**] 對話方塊中，選取資料來源，或定義新的資料來源。  
  
        2.  輸入將包含查詢結果之資料表的名稱。  
  
        3.  使用選項，**加入至 DSV**，以建立資料表，並將它新增至現有的資料來源檢視。 如果您想要在相同的資料來源檢視中保留模型的所有相關資料表 (例如定型資料、預測來源資料和查詢結果)，這樣做就很有用。  
  
        4.  使用選項，**時，覆寫存在**、 使用最新的結果來更新現有的資料表。  
  
             如果您已將任何資料行加入至預測查詢、變更預測查詢中任何資料行的名稱或資料類型，或者已針對目的地資料表執行任何 ALTER 陳述式，就必須使用此選項來覆寫資料表。  
  
             此外，如果多個資料行具有相同的名稱 (例如，預設資料行名稱**運算式**) 您必須建立資料行的別名名稱重複，或當設計師嘗試將結果儲存至 SQL，就會引發錯誤伺服器。 原因是 SQL Server 不允許多個資料行具有相同的名稱。  
  
             如需詳細資訊，請參閱 <<c0> [ 儲存資料採礦查詢結果對話方塊&#40;採礦模型預測檢視&#41;](../../2014/analysis-services/save-data-mining-query-result-dialog-box-mining-model-prediction-view.md)。</c0>  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [使用鑽研結構資料上&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/using-drillthrough-on-structure-data-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用預測查詢產生器來建立預測查詢](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
