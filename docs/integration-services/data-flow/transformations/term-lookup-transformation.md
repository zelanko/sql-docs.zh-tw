---
title: "詞彙查閱轉換 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.termlookuptrans.f1
- sql13.dts.designer.termlookup.termlookup.f1
- sql13.dts.designer.termlookup.referencetable.f1
- sql13.dts.designer.termlookup.advanced.f1
helpviewer_keywords:
- extracting data [Integration Services]
- match extracted terms [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- lookups [Integration Services]
- counting extracted items
- Term Lookup transformation
ms.assetid: 3c0fa2f8-cb6a-4371-b184-7447be001de1
caps.latest.revision: 56
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: ee1fa267107940169c05942e8614a7bf7148566a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/19/2017

---
# <a name="term-lookup-transformation"></a>詞彙查閱轉換
  「詞彙查閱」轉換會比對從轉換輸入資料行的文字中擷取的詞彙，以及參考資料表中的詞彙。 然後，它會計算查閱資料表中的詞彙在輸入資料集中出現的次數，並將計數與參考資料表的詞彙一起寫入轉換輸出中的資料行。 此轉換包括單字頻率統計資料，對基於輸入文字建立自訂單字清單很有用處。  
  
 在「詞彙查閱」轉換執行查閱之前，它會使用與「詞彙擷取」轉換相同的方法從輸入資料行的文字中擷取單字：  
  
-   文字分解為句子。  
  
-   句子分解為單字。  
  
-   單字會正規化。  
  
 若要進一步自訂要比對的詞彙，可以設定「詞彙查閱」轉換，以執行區分大小寫的比對。  
  
## <a name="matches"></a>比對  
 「詞彙查閱」會使用下列規則執行查閱並傳回值：  
  
-   如果設定轉換執行區分大小寫的比對，則會捨棄使區分大小寫比較失敗的比對。 例如，會將 *student* 及 *STUDENT* 視為不同的單字。  
  
    > [!NOTE]  
    >  未大寫的單字可與在句子開頭大寫的單字進行比對。 例如，當 *Student* 為句子第一個單字時， *student* 與 *Student* 之間的比對則會成功。  
  
-   如果名詞或名詞片語的複數形式存在於參考資料表中，則查閱只會比對名詞或名詞片語的複數形式。 例如， *students* 的所有執行個體都會在 *student*的執行個體之外另行計數。  
  
-   如果在參考資料表中找到單字的單數形式，則單字或片語的單數及複數形式都會與單數形式比對。 例如，如果查閱資料表包含 *student*，且轉換找到單字 *student* 及 *students*，則會將這兩個單字作為查閱詞彙 *student*的相符部份進行計數。  
  
-   如果輸入資料行中的文字是還原的名詞片語，則只有該名詞片語中的最後一個單字會受正規化影響。 例如， *doctors appointments* 的還原版本是 *doctors appointment*。  
  
 當查閱項目在參考集中包含重疊的詞彙 (即，在一個以上參考記錄中找到子詞彙) 時，「詞彙查閱」轉換只會傳回一個查閱結果。 下列範例顯示查閱項目包含重疊子詞彙時的結果。 此處的重疊子詞彙為 *Windows*，其在兩個參考詞彙中均有找到。 但轉換不會傳回兩個結果，而只會傳回單一參考詞彙 *Windows*。 第二個參考詞彙 *Windows 7 Professional*不會傳回。  
  
|項目|Value|  
|----------|-----------|  
|輸入詞彙|Windows 7 Professional|  
|參考詞彙|Windows、Windows 7 Professional|  
|輸出|Windows|  
  
 「詞彙查閱」轉換可以比對包含特殊字元的名詞及名詞片語，且參考資料表中的資料可能包含這些字元。 特殊字元，如下所示為: %，@，&、 $、 #、 \*，:，;，。， **，** ，！，？， \<，>，+、 =、 ^、 ~，|， \\，/，（、）、 [、]、 {、}、"，和 '。  
  
## <a name="data-types"></a>資料型別  
 「詞彙查閱」轉換只可以使用具有 DT_WSTR 或 DT_NTEXT 資料類型的資料行。 如果資料行包含文字，但不具有這些資料類型的其中之一，則「資料轉換」可以將具有 DT_WSTR 或 DT_NTEXT 資料類型的資料行加入資料流程，並將資料行值複製至新資料行。 然後，「資料轉換」的輸出可以用作「詞彙查閱」轉換的輸入。 如需詳細資訊，請參閱 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)。  
  
## <a name="configuration-the-term-lookup-transformation"></a>設定詞彙查閱轉換  
 「詞彙查閱」轉換輸入資料行包含可指出資料行用法的 InputColumnType 屬性。 InputColumnType 可包含下列值：  
  
-   值 0 表示資料行只傳遞至輸出，且不在查閱中使用。  
  
-   值 1 表示資料行只在查閱中使用。  
  
-   值 2 表示資料行傳遞至輸出，且亦在查閱中使用。  
  
 InputColumnType 屬性設為 0 或 2 的轉換輸出資料行包含資料行的 CustomLineageID 屬性，其包含上游資料流程元件指派給該資料行的歷程識別碼。  
  
 「詞彙查閱」轉換會將兩個資料行新增到轉換輸出，以預設的 **Term** 和 **Frequency**來命名。 **Term** 包含了查閱資料表中的詞彙，而 **Frequency** 包含了參考資料表中的詞彙發生在輸入資料集內的次數。 這些資料行不包含 CustomLineageID 屬性。  
  
 查閱資料表必須是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 Access 資料庫中的資料表。 如果將「詞彙擷取」轉換的輸出儲存為資料表，不僅可將此資料表用為參考資料表，也可以使用其他資料表。 在您可以使用「詞彙查閱」轉換之前，一般檔案、Excel 活頁簿或其他來源中的文字必須匯入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫或 Access 資料庫。  
  
 「詞彙查閱」轉換會使用個別 OLE DB 連接，以連接到參考資料表。 如需詳細資訊，請參閱 [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
 「詞彙查閱」轉換以完全預先快取模式運作。 在執行階段，「詞彙查閱」轉換在處理任何轉換輸入資料列之前，會從參考資料表讀取詞彙，並將其儲存於其私用記憶體中。  
  
 因為輸入資料行資料列中的詞彙可能重複，所以「詞彙查閱」轉換的輸出一般比轉換輸入擁有更多的資料列。  
  
 轉換擁有一項輸入和一項輸出， 但它不支援錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="term-lookup-transformation-editor-term-lookup-tab"></a>詞彙查閱轉換編輯器 (詞彙查閱索引標籤)
  使用 **[詞彙查閱轉換編輯器]** 對話方塊的 **[詞彙查閱]** 索引標籤，即可將輸入資料行對應至參考資料表的查閱資料行，並提供每一個輸出資料行的別名。  
  
### <a name="options"></a>選項  
 **可用輸入資料行**  
 使用核取方塊選取輸入資料行，即可讓這些輸入資料行在不變更的狀況下通過至輸出。 將輸入資料行拖曳至 **[可用的參考資料行]** 清單，即可對應至參考資料表的查閱資料行。 輸入和查閱資料行都必須有相符、受支援的資料類型，包括 DT_NTEXT 或 DT_WSTR。 在 [ [建立關聯性](../../../integration-services/data-flow/transformations/create-relationships.md) ] 對話方塊中選取對應行，並以滑鼠右鍵按一下來編輯對應。  
  
 **可用的參考資料行**  
 檢視參考資料表中可用的資料行。 選擇包含要比對之詞彙清單的資料行。  
  
 **通過資料行**  
 從可用的輸入資料行清單中選取。 您的選擇會反映在 **[可用的輸入資料行]** 資料表的核取方塊選擇中。  
  
 **輸出資料行別名**  
 輸入每一個輸出資料行的別名。 預設為資料行的名稱；不過，您可以選擇任何唯一的描述性名稱。  
  
 **設定錯誤輸出**  
 使用 [ [設定錯誤輸出](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ] 對話方塊，即可指定造成錯誤之資料列的錯誤處理選項。  
  
## <a name="term-lookup-transformation-editor-reference-table-tab"></a>詞彙查閱轉換編輯器 (參考資料表索引標籤)
  使用 [詞彙查閱轉換編輯器] 對話方塊的 [參考資料表] 索引標籤，即可指定參考 (查閱) 資料表的連接。  
  
### <a name="options"></a>選項。  
 **OLE DB 連接管理員**  
 從清單中選取現有的連線管理員，或按一下 [新增] 來建立新的連線。  
  
 **新**  
 使用 [設定 OLE DB 連線管理員] 對話方塊來建立新的連線。  
  
 **參考資料表名稱**  
 從清單中選取項目，以選取資料庫中的查閱資料表或檢視。 資料表或檢視應包含具有現有詞彙清單的資料行，可以用來與來源資料行中的文字進行比較。  
  
 **設定錯誤輸出**  
 使用 [ [設定錯誤輸出](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ] 對話方塊，即可指定造成錯誤之資料列的錯誤處理選項。  
  
## <a name="term-lookup-transformation-editor-advanced-tab"></a>詞彙查閱轉換編輯器 (進階索引標籤)
  使用 [詞彙查閱轉換編輯器] 對話方塊的 [進階] 索引標籤，即可指定查閱是否應區分大小寫。  
  
### <a name="options"></a>選項  
 **使用區分大小寫的詞彙查閱**  
 指出查閱是否區分大小寫。 預設值為 **False**。  
  
 **設定錯誤輸出**  
 使用 [ [設定錯誤輸出](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ] 對話方塊，即可指定造成錯誤之資料列的錯誤處理選項。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../../integration-services/integration-services-error-and-message-reference.md)   
 [詞彙擷取轉換](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  

