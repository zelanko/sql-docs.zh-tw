---
title: 將串聯參數新增至報表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 3a22eec3-57a7-478e-b6fc-102a9dbe0591
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cc7ac8634ab77d7648326e5a7e2762d758fb78c9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106694"
---
# <a name="add-cascading-parameters-to-a-report-report-builder-and-ssrs"></a>將串聯參數加入至報表 (報表產生器及 SSRS)
  串聯參數會提供管理大量報表資料的方法。 您可以定義一組相關的參數，讓某一個參數的值清單會視另一個參數所選擇的值而定。 例如，第一個參數是獨立的，而且可能代表一個產品類別目錄的清單。 使用者選取類別目錄時，第二個參數會相依於第一個參數的值。 其值會隨著所選類別目錄內的子類別目錄清單更新。 當使用者檢視報表時，類別目錄與子類別目錄參數的值都用於篩選報表資料。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 若要建立串聯參數，您要先定義資料集查詢，然後加入所需之每個串聯參數的查詢參數。 您也必須針對每個串聯參數建立個別的資料集來提供可用的值。 如需詳細資訊，請參閱[為報表參數新增、變更或刪除可用的值 &#40;報表產生器和 SSRS&#41;](add-change-or-delete-available-values-for-a-report-parameter.md)。  
  
 順序對於串聯參數相當重要，因為列在清單中後面之參數的資料集查詢會包含清單中前面每個參數的參考。 在執行階段，參數在 [報表資料] 窗格中的順序會決定參數查詢出現在報表中的順序，因此，也會決定使用者選擇每個後續參數值的順序。  
  
 如需有關使用多個值 (包含全選功能) 建立串聯式參數的詳細資訊，請參閱 [如何擁有全選多值的串聯式參數](https://go.microsoft.com/fwlink/?LinkId=184757)。  
  
### <a name="to-create-the-main-dataset-with-a-query-that-includes-multiple-related-parameters"></a>若要利用包含多個相關參數的查詢建立主資料集  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下資料來源，然後按一下 **[加入資料集]** 。  
  
2.  在 **[名稱]** 中，輸入資料集的名稱。  
  
3.  在 **[資料來源]** 中，選擇資料來源的名稱，或是按一下 **[新增]** 來建立一個名稱。  
  
4.  在 **[查詢類型]** 中，選擇所選資料來源的查詢類型。 在本主題中，會假設 **[文字]** 查詢類型。  
  
5.  在 **[查詢]** 中，輸入用於擷取此報表之資料的查詢。 查詢必須包括下列部分：  
  
    1.  資料來源欄位的清單。 例如，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中，SELECT 陳述式會指定給定資料表或資料列中的資料庫資料行名稱清單。  
  
    2.  適用於每個串聯參數的一個查詢參數。 查詢參數會指定要在查詢中包含或排除的特定值，藉以限制從資料來源擷取的資料。 查詢參數通常出現在查詢的限制子句中。 例如，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 陳述式中，查詢參數會出現在 WHERE 子句中。 如需詳細資訊，請參閱《 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SQL Server 線上叢書 [》中](https://go.microsoft.com/fwlink/?linkid=120955)文件集的＜使用 WHERE 和 HAVING 篩選資料列＞。  
  
6.  按一下 **[執行]** ( **!** )。 加入查詢參數然後執行查詢之後，會自動建立對應到查詢參數的報表參數。  
  
    > [!NOTE]  
    >  您第一次執行查詢時，查詢參數的順序會決定這些參數在報表中建立的順序。 若要變更順序，請參閱[變更報表參數的順序 &#40;報表產生器及 SSRS&#41;](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 下一步，您將建立資料集，提供獨立參數的值。  
  
### <a name="to-create-a-dataset-to-provide-values-for-an-independent-parameter"></a>建立資料集以提供獨立參數的值  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下資料來源，然後按一下 **[加入資料集]** 。  
  
2.  在 **[名稱]** 中，輸入資料集的名稱。  
  
3.  在 **[資料來源]** 中，確認名稱為您在步驟 1 中選擇之資料來源的名稱。  
  
4.  在 **[查詢類型]** 中，選擇所選資料來源的查詢類型。 在本主題中，會假設 **[文字]** 查詢類型。  
  
5.  在 **[查詢]** 中，輸入用於擷取此參數之值的查詢。 獨立參數的查詢通常不包含查詢參數。 例如，若要建立提供所有類別目錄值之參數的查詢，您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，類似如下：  
  
    ```  
    SELECT DISTINCT <column name> FROM <table>  
    ```  
  
     SELECT DISTINCT 命令會從結果集移除重複的值，讓您可以從指定之資料表的指定資料行中取得每個唯一的值。  
  
     按一下 **[執行]** ( **!** )。 結果集會顯示可用於這個第一個參數的值。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 下一步，您將設定第一個參數的屬性，以便在執行階段使用此資料集擴展其可用的值。  
  
### <a name="to-set-available-values-for-a-report-parameter"></a>設定報表參數的可用值  
  
1.  在 [報表資料] 窗格的 [參數] 資料夾中，以滑鼠右鍵按一下第一個參數，然後按一下 **[參數屬性]** 。  
  
2.  在 **[名稱]** 中，確認參數的名稱正確。  
  
3.  按一下 **[可用的值]** 。  
  
4.  按一下 **[從查詢取得值]** 。 三個欄位隨即出現。  
  
5.  在 **[資料集]** 中，從下拉式清單按一下您在先前程序中建立之資料集的名稱。  
  
6.  在 **[值]** 欄位中，按一下提供參數值之欄位的名稱。  
  
7.  在 **[標籤]** 欄位中，按一下提供參數標籤之欄位的名稱。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 下一步，您將建立資料集，提供相依參數的值。  
  
### <a name="to-create-a-dataset-to-provide-values-for-a-dependent-parameter"></a>建立資料集以提供相依參數的值  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下資料來源，然後按一下 **[加入資料集]** 。  
  
2.  在 **[名稱]** 中，輸入資料集的名稱。  
  
3.  在 **[資料來源]** 中，確認名稱為您在步驟 1 中選擇之資料來源的名稱。  
  
4.  在 **[查詢類型]** 中，選擇所選資料來源的查詢類型。 在本主題中，會假設 **[文字]** 查詢類型。  
  
5.  在 **[查詢]** 中，輸入用於擷取此參數之值的查詢。 相依參數的查詢通常包含查詢參數，以供此參數所相依的每個參數使用。 例如，若要建立針對某個類別目錄 (獨立參數) 提供所有子類別目錄 (相依參數) 值之參數的查詢，您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，類似如下：  
  
    ```  
    SELECT DISTINCT Subcategory FROM <table>   
    WHERE (Category = @Category)  
    ```  
  
     在 WHERE 子句中，[類別目錄] 是 \<資料表> 的欄位名稱，而 @Category 則是查詢參數。 此陳述式會針對在 @Category 中指定的類別目錄，產生子類別目錄的清單。 在執行階段，系統會利用使用者針對報表參數選擇的同名值填入此值。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 下一步，您將設定第二個參數的屬性，以便在執行階段使用此資料集擴展其可用的值。  
  
### <a name="to-set-available-values-for-a-report-parameter"></a>設定報表參數的可用值  
  
1.  在 [報表資料] 窗格的 [參數] 資料夾中，以滑鼠右鍵按一下第一個參數，然後按一下 **[參數屬性]** 。  
  
2.  在 **[名稱]** 中，確認參數的名稱正確。  
  
3.  按一下 **[可用的值]** 。  
  
4.  按一下 **[從查詢取得值]** 。  
  
5.  在 **[資料集]** 中，從下拉式清單按一下您在先前程序中建立之資料集的名稱。  
  
6.  在 **[值]** 欄位中，按一下提供參數值之欄位的名稱。  
  
7.  在 **[標籤]** 欄位中，按一下提供參數標籤之欄位的名稱。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-test-the-cascading-parameters"></a>測試串聯參數  
  
1.  按一下 **[執行]** 。  
  
2.  從第一個獨立參數的下拉式清單中選擇一個值。  
  
     報表處理器會執行下一個參數的資料集查詢，並傳遞您針對第一個參數選擇的值。 第二個參數的下拉式清單會根據第一個參數值，以可用的值擴展。  
  
3.  從第二個相依參數的下拉式清單中選擇一個值。  
  
     報表不會在選擇最後一個參數後自動執行，因此您可以變更您的選擇。  
  
4.  按一下 **[檢視報表]** 。 報表會根據您所選擇的參數，更新顯示。  
  
## <a name="see-also"></a>另請參閱  
 [加入、變更或刪除報表參數 &#40;報表產生器及 SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [報表參數 &#40;報表產生器和報表設計師&#41;](report-parameters-report-builder-and-report-designer.md)   
 [教學課程：將參數新增至報表 &#40;報表產生器&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [教學課程 &#40;報表產生器&#41;](../report-builder-tutorials.md)   
 [新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
