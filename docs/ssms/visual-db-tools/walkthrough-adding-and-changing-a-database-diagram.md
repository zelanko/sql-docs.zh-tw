---
title: "逐步解說：加入與變更資料庫圖表 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database diagrams [SQL Server], about database diagrams
- database diagrams [SQL Server], designing
- database diagrams [SQL Server], creating
ms.assetid: 228caa0d-8f24-46ab-86d1-b6d8631322bc
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7835747f81513f26fb7e69a357094cdc1d8dcfe0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="walkthrough-adding-and-changing-a-database-diagram"></a>逐步解說：加入與變更資料庫圖表
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 這個逐步解說將說明如何建立與修改資料庫圖表，以及透過資料庫圖表元件對資料庫進行變更。 您將看到如何將資料表加入至圖表、建立資料表之間的關聯性、建立資料行上的條件約束和索引，以及變更您查看每個資料表的資訊層級。  
  
## <a name="prerequisites"></a>Prerequisites  
為了完成這個逐步解說，您需要：  
  
-   存取含有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 範例資料庫的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)]  
  
-   具有資料庫擁有者 **dbo** 權限的帳戶  
  
> [!NOTE]  
> 如果沒有足夠權限的帳戶，嘗試對資料表進行變更時，就會出現錯誤訊息。  
  
## <a name="creating-a-diagram"></a>建立圖表  
  
#### <a name="to-create-a-new-database-diagram"></a>若要建立新的資料庫圖表  
  
1.  在 [檢視] 功能表上，按一下 [物件總管]。  
  
2.  開啟 [資料庫] 節點，然後開啟 [[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)]] 節點。  
  
3.  以滑鼠右鍵按一下 [資料庫圖表] 節點，再選擇 [新增資料庫圖表]。  
  
    如果資料庫沒有建立圖表所需的物件，便會顯示下列訊息：**此資料庫沒有使用資料庫圖表所需的一或多個支援物件。要建立資料庫物件嗎?** 選擇 [ **是**]。  
  
    出現 [新增資料表] 對話方塊。  
  
4.  選取 [AddressType (Person)] 和 [Address (Person)]，然後按一下 [新增]。  
  
    兩個資料表便會加入至圖表。  
  
5.  關閉 [新增資料表] 對話方塊。  
  
#### <a name="to-view-different-column-data"></a>若要檢視不同的資料行資料  
  
1.  以滑鼠右鍵按一下 `Address` 資料表。 在快速鍵功能表上，指向 [資料表檢視]，然後按一下 [標準]。  
  
    資料表方格會顯示三個資料行：[資料行名稱]、[資料類型] 和 [允許 Null]。  
  
2.  以滑鼠右鍵按一下 `Address` 資料表、按一下 [資料表檢視]，再選取 [索引鍵]。  
  
    資料表方格會顯示一個資料行，內含資料表資料行名稱。 只有那些參與索引的資料行才會出現。  
  
## <a name="creating-new-tables"></a>建立新資料表  
  
#### <a name="to-create-tables-within-diagram-designer"></a>若要在圖表設計工具中建立資料表  
  
1.  以滑鼠右鍵按一下現有資料表外側的 [圖表設計工具]，再選擇 [新增資料表]。  
  
2.  在 [選擇名稱] 對話方塊中，按一下 [確定]，接受預設名稱 **Table1**。  
  
    隨即出現新的資料表方格，其中會有三個資料行：[資料行名稱]、[資料類型] 和 [允許 Null]。  
  
3.  將下列資訊新增至 **Table1**：  
  
    |**資料行名稱**|**資料類型**|**允許 Null**|  
    |-------------------|-----------------|-------------------|  
    |**T1col1**|**int**|已選取|  
    |**T1col2**|**varchar(50)**|已選取|  
    |**T1col3**|**float**|已選取|  
  
4.  以滑鼠右鍵按一下 `T1col1`，再選取 [設定主索引鍵]。  
  
    資料行名稱旁邊將會出現索引鍵圖示。  
  
5.  從 [檔案] 功能表中按一下 [儲存 Diagram1]。  
  
6.  在 [選擇名稱] 對話方塊中，按一下 [確定]，接受預設名稱 **Diagram1**。  
  
7.  [儲存] 對話方塊會顯示訊息，表示要將 `Table1` 儲存到資料庫。 按一下 **[是]**。  
  
## <a name="modifying-table-structure"></a>修改資料表結構  
您可以在圖表設計工具中加入檢查條件約束，以及建立資料表間的關聯性。  
  
#### <a name="to-create-check-constraints"></a>若要建立檢查條件約束  
  
1.  在 `Table1` 中，以滑鼠右鍵按一下 `T1col3` 資料列，再選擇 [檢查條件約束]。  
  
    此時會出現 [檢查條件約束] 對話方塊。  
  
2.  按一下 **[加入]**。  
  
    [選取的檢查條件約束] 清單中會出現新的條件約束，其預設名稱為 `CK_Table1`。  
  
3.  選取方格中的 [運算式] 資料列，然後按一下省略符號按鈕。  
  
    [檢查條件約束運算式] 對話方塊便會出現。  
  
4.  輸入 **T1col3 > 5** 然後按一下 [確定]。  
  
    `Table1` 現在便會有一項條件約束，規定所有輸入 `T1col3` 的值都必須大於 5。  
  
5.  按一下 [ **關閉**]。  
  
#### <a name="to-create-relationships-between-tables"></a>若要建立資料表之間的關聯性  
  
1.  在圖表設計工具中建立新資料表，將其命名為 `Table2` ，並且包含下列資料行：  
  
    |**資料行名稱**|**資料類型**|**允許 Null**|  
    |-------------------|-----------------|-------------------|  
    |**T2col1**|**int**|未選取|  
    |**T2col2**|**varchar(50)**|已選取|  
    |**T2col3**|**xml**|已選取|  
  
    > [!NOTE]  
    > 外部索引鍵關聯性的主索引鍵端的資料行必須加入主索引鍵或唯一的條件約束。  
  
2.  將 `T2col1` 拖曳到 `T1col1`。  
  
    會出現兩個對話方塊：背景中的 [外部索引鍵關聯性] 以及前景中的 [資料表與資料行]。  
  
3.  按一下 [確定] 以儲存新的關聯性。  
  
4.  再按一下 [確定]。  
  
## <a name="creating-indexes"></a>建立索引  
您可以在大部分的資料類型上建立索引，包括 XML。  
  
#### <a name="to-create-a-standard-index"></a>若要建立標準索引  
  
1.  以滑鼠右鍵按一下 `Table1`，再選擇 [索引/索引鍵]。  
  
    [索引/索引鍵] 對話方塊便會出現。  
  
2.  按一下 **[加入]**。  
  
    [選取的主/唯一索引鍵或索引] 清單中會出現新的索引，其預設名稱類似 `IX_Table1`。  
  
3.  選取 [資料行] 資料列，然後按一下省略符號按鈕。  
  
    [索引資料行] 對話方塊便會出現。  
  
4.  按一下 [資料行名稱] 下方的下拉箭頭，然後選取 `T1col2`。  
  
    > [!NOTE]  
    > 您選取 `T1col2` 下面的資料格，再選擇另一個資料行名稱，即可將其他資料行加入至這個索引。  
  
5.  按一下 [確定] 以儲存這個索引。  
  
6.  按一下 [索引/索引鍵] 對話方塊中的 [關閉]。  
  
#### <a name="to-create-an-xml-index"></a>若要建立 XML 索引  
  
1.  以滑鼠右鍵按一下 `T2col1`，再選擇 [設定主索引鍵]。  
  
    > [!NOTE]  
    > 加入 XML 索引時，需要將資料表中的另一個資料行設定為叢集主索引鍵。  
  
2.  以滑鼠右鍵按一下 `Table2` 中的 `T2col3` 資料列，再選取 [XML 索引]。  
  
    [XML 索引] 對話方塊便會出現。  
  
3.  按一下 **[加入]**。  
  
    便會將含有預設值的 XML 索引新增至 [選取的 XML 索引] 清單。  
  
4.  按一下 [ **關閉**]。  
  
    > [!NOTE]  
    > XML 索引會針對個別資料行建立。 第一個 XML 索引是主索引；任何額外的索引則為次要索引。  
  
## <a name="saving-the-diagram"></a>儲存圖表  
您對圖表所做的變更要等到儲存之後，才會傳送到資料庫。 如果有問題或衝突發生，就會顯示帶有詳細資訊的對話方塊。  
  
#### <a name="to-save-a-database-diagram"></a>若要儲存資料庫圖表  
  
1.  在 [檔案] 功能表上選取 [儲存 Diagram1]。  
  
    此時會出現 [儲存] 對話方塊。 如果選取了 [受影響資料表的警告]，便會列出有關新的或變更的資料表的資訊。  
  
2.  按一下 [確定] 。  
  
3.  如果發生任何錯誤，[儲存後告知] 對話方塊會顯示錯誤及其原因。 修正錯誤並再一次儲存圖表。  
  
## <a name="next-steps"></a>Next Steps  
這是含有兩個現有的及兩個新的資料表的基本圖表，但是已經具體而微地說明其圖表化現有資料庫或透過視覺化方式建立新結構描述的潛力。 建議您進一步研究的部分包括：  
  
-   建立含有相關資料表群組的新圖表  
  
-   自訂每個資料表顯示的資訊數量  
  
-   變更配置以及加入註解  
  
-   將圖表複製為點陣圖  
  
## <a name="see-also"></a>另請參閱  
[自訂圖表中顯示的資料量 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md)  
[設定資料庫圖表設計工具 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
[將資料表新增至圖表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
[在圖表上建立資料表之間的關聯性 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-relationships-between-tables-on-a-diagram-visual-database-tools.md)  
[建立 XML 索引](http://msdn.microsoft.com/en-us/6ecac598-355d-4408-baf7-1b2e8d4cf7c1)  
[複製資料庫圖表的影像到剪貼簿 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/copy-an-image-of-a-database-diagram-to-the-clipboard-visual-database-tools.md)  
[使用圖表配置 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-diagram-layout-visual-database-tools.md)  
  
