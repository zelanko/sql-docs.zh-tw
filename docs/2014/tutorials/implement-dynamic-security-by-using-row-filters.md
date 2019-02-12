---
title: 使用資料列篩選實作動態安全性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8bf03c45-caf5-4eda-9314-e4f8f24a159f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5a26f9c950dd09b8e47c83089415bd2b3d47458f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041049"
---
# <a name="implement-dynamic-security-by-using-row-filters"></a>使用資料列篩選器實作動態安全性
  在這個補充課程中，您將建立實作動態安全性的其他角色。 動態安全性提供以使用者目前登入的使用者名稱或登入識別碼為主的資料列層級安全性。 如需詳細資訊，請參閱[角色 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/roles-ssas-tabular.md)。  
  
 若要實作動態安全性，您必須將資料表加入至包含 Windows 使用者名稱的模型，這些使用者可以建立與模型的連接做為資料來源並且瀏覽模型物件與資料。 您使用本教學課程建立的模型位於 Adventure Works Corp. 內容中；不過為了完成本課程，您必須加入包含您自己的網域使用者的資料表。 您將不需要所加入使用者名稱的密碼。 若要 Employee Security 資料表，其中包含幾個您網域中的範例使用者，您將使用 [貼上] 功能從 Excel 試算表貼入員工資料。 在真實情況中，包含您加入模型中之使用者名稱的資料表通常會使用來自實際資料庫的資料表做為資料來源；例如，實際的 dimEmployee 資料表。  
  
 若要實作動態安全性，您會使用兩個新的 DAX 函式：[USERNAME 函式&#40;DAX&#41; ](https://msdn.microsoft.com/library/hh230954.aspx)並[LOOKUPVALUE 函式&#40;DAX&#41;](https://msdn.microsoft.com/library/gg492170.aspx)。 這兩個函數是在新角色中定義，並且會套用至資料列篩選器公式。 該公式會使用 LOOKUPVALUE 函數從 Employee Security 資料表指定一個值，然後將該值傳遞給 USERNAME 函數，此函數會指定登錄使用者的使用者名稱屬於此角色。 使用者可以再瀏覽該角色的資料列篩選器所指定的資料。 在這個案例中，您將指定銷售員工只能瀏覽本身所屬銷售地區的網際網路銷售資料。  
  
 您將要完成一系列工作，才能完成這個補充課程。 例如此 Adventure Works 表格式模型案例專屬的工作就是這類工作，但不一定適用於真實案例。 每一項工作都包含描述工作目的的其他資訊。  
  
 完成本課程的估計時間：**30 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
 這個補充課程主題是表格式模型教學課程的一部分，必須依序完成。 在執行本補充課程中的工作之前，您應已完成之前所有課程。  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>將 dimSalesTerritory 資料表加入至 AW Internet Sales 表格式模型專案  
 若要實作此 Adventure Works 案例的動態安全性，您必須在模型中加入兩個額外的資料表。 第一個要加入的資料表是來自相同 AdventureWorksDW 資料庫的 dimSalesTerritory (也就是銷售地區)。 稍後您將在 Sales Territory 資料表中套用資料列篩選器，以定義登入的使用者可以瀏覽的特定資料。  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>若要加入 dimSalesTerritory 資料表  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[現有連接]**。  
  
2.  在 [現有連接] 對話方塊中，確認已選取 [Adventure Works DB from SQL] 資料來源連接，然後按一下 [開啟]。  
  
     如果出現 [模擬認證] 對話方塊中，輸入您所使用的模擬認證在第 2 課：加入資料。  
  
3.  在 [選擇如何匯入資料] 頁面上，讓 [從資料表和檢視表清單來選取要匯入的資料] 保持選取狀態，然後按一下 [下一步]。  
  
4.  在 [選取資料表和檢視表] 頁面上，選取 [DimSalesTerritory] 資料表。  
  
5.  在 [易記名稱] 資料行中，輸入 **Sales Territory**。  
  
6.  按一下 [預覽和篩選]。  
  
7.  取消選取 [SalesTerritoryAlternateKey] 資料行，然後按一下 [確定]。  
  
8.  在 [選取資料表和檢視表] 頁面上，按一下 [完成]。  
  
     新的資料表將會加入至模型工作空間。 來源 dimSalesTerritory 資料表中的物件和資料隨後將匯入 AW Internet Sales 表格式模型的新 Sales Territory 資料表中。  
  
9. 匯入資料表之後，按一下 [關閉]。  
  
## <a name="give-the-columns-friendly-names"></a>為資料行指定易記名稱  
 在這項工作中，您將重新命名 Sales Territory 資料表中的資料行，為其指定易記名稱。 不一定要為資料表及/或資料行提供易記名稱，不過，它的確可以讓您的模型專案更容易在模型設計工具中進行導覽，並可讓使用者瀏覽用戶端應用程式欄位清單中的模型物件和資料。  
  
#### <a name="to-rename-columns-in-the-sales-territory-table"></a>若要重新命名 Sales Territory 資料表中的資料行  
  
-   在模型設計師中，重新命名 **Sales Territory** 資料表中的資料行：  
  
     **銷售領域**  
  
    |來源名稱|易記名稱|  
    |-----------------|-------------------|  
    |SalesTerritoryKey|Sales Territory Id|  
    |SalesTerritoryRegion|Sales Territory Region|  
    |SalesTerritoryCountry|Sales Territory Country|  
    |SalesTerritoryGroup|Sales Territory Group|  
  
## <a name="add-a-table-with-user-name-data"></a>加入包含使用者名稱資料的資料表  
 由於 AdventureWorksDW 範例資料庫中的 dimEmployee 資料表包含來自 AdventureWorks 網域的使用者，而這些使用者名稱並不存在您自己的環境中，因此您必須在模型中建立包含幾個 (三個) 您組織中實際使用者的資料表。 之後您會加入這些使用者做為新角色的成員。 您不需要範例使用者名稱的密碼，但是需要您自己網域中的實際 Windows 使用者名稱。  
  
#### <a name="to-add-an-employee-security-table"></a>若要加入 Employee Security 資料表  
  
1.  開啟 Microsoft Excel，建立一個新的工作表。  
  
2.  複製下列資料表，包括標頭資料列，然後將它貼入工作表中。  
  
    |Employee Id|Sales Territory Id|First Name|Last Name|Login Id|  
    |-----------------|------------------------|----------------|---------------|--------------|  
    |1|2|\<使用者第一個名稱 >|\<使用者的最後一個名稱 >|\<domain\username>|  
    |1|3|\<使用者第一個名稱 >|\<使用者的最後一個名稱 >|\<domain\username>|  
    |2|4|\<使用者第一個名稱 >|\<使用者的最後一個名稱 >|\<domain\username>|  
    |3|5|\<使用者第一個名稱 >|\<使用者的最後一個名稱 >|\<domain\username>|  
  
3.  在新的工作表中，將 first name、last name 和 domain\username 取代為您組織中三個使用者的姓名和登入識別碼。 在 Employee Id 1 的前兩個資料列中放入相同的使用者。 這樣表示這個使用者屬於多個銷售地區。 Employee Id 和 Sales Territory Id 欄位保持不變。  
  
4.  儲存為工作表`Sample Employee`。  
  
5.  在該工作表中，選取所有包含員工資料的資料格 (包括標頭)，然後以滑鼠右鍵按一下選取的資料，再按一下 [複製]。  
  
6.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，按一下 [編輯] 功能表，然後按一下 [貼上]。  
  
     如果 [貼上] 呈現灰色，請按一下模型設計師視窗中任何資料表的任何資料行，然後按一下 [編輯] 功能表，再按一下 [貼上]。  
  
7.  在 **貼上預覽**對話方塊中，於**資料表名稱**，型別`Employee Security`。  
  
8.  在 [要貼上的資料] 中，確認資料包含 Sample Employee 工作表中的所有使用者資料和標頭。  
  
9. 確認已核取 [使用第一個資料列作為資料行標頭]，然後按一下 [確定]。  
  
     這樣就會建立名為 Employee Security 的新資料表，其中包含從 Sample Employee 工作表複製的員工資料。  
  
## <a name="create-relationships-between-internet-sales-geography-and-sales-territory-table"></a>在 Internet Sales、Geography 和 Sales Territory 資料表之間建立關聯性  
 Internet Sales、Geography 和 Sales Territory 資料表全都包含常用的資料行 Sales Territory Id。Sales Territory 資料表中的 Sales Territory Id 資料行包含值，每個銷售地區都有不同的識別碼。  
  
#### <a name="to-create-relationships-between-the-internet-sales-geography-and-the-sales-territory-table"></a>若要在 Internet Sales、Geography 和 Sales Territory 資料表之間建立關聯性  
  
1.  在模型設計師中，於 [圖表檢視] 的 [Geography] 資料表中按住 [Sales Territory Id] 資料行，然後將資料指標拖曳至 [Sales Territory] 資料表的 [Sales Territory Id] 資料行中，再放開。  
  
2.  在 [Internet Sales] 資料表中，按住 [Sales Territory Id] 資料行，然後將資料指標拖曳至 [Sales Territory] 資料表的 [Sales Territory Id] 資料行中，再放開。  
  
     請注意，此關聯性的 [作用中] 屬性為 False，表示它為非作用中。 這是因為 Internet Sales 資料表已有另一個在量值中使用的作用中關聯性。  
  
## <a name="hide-the-employee-security-table-from-client-applications"></a>對用戶端應用程式隱藏 Employee Security 資料表  
 在這個工作中，您將隱藏 Employee Security 資料表，使其不會出現在用戶端應用程式欄位清單。 請記住，隱藏資料表並不會保護其安全。 使用者仍然可以查詢 Employee Security 資料表的資料 (如果使用者知道如何查詢的話)。 為了保護 Employee Security 資料表資料的安全，防止使用者查詢其中的任何資料，您將在稍後的工作中套用篩選器。  
  
#### <a name="to-hide-the-employee-table-from-client-applications"></a>若要對用戶端應用程式隱藏 Employee 資料表  
  
-   在模型設計師的 [圖表檢視] 中，以滑鼠右鍵按一下 [Employee] 資料表標題，然後按一下 [在用戶端工具中隱藏]。  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>建立 Sales Employees by Territory 使用者角色  
 在這項工作中，您將建立新的使用者角色。 這個角色將包含一個資料列篩選器，用於定義使用者可以看見 Sales Territory 資料表中的哪些資料列。 這個篩選器隨後會在一對多關聯性方向中套用至與 Sales Territory 相關的所有其他資料表。 您還會套用一個簡單的篩選器，用來保護整個 Employee Security 資料表的安全，防止屬於該角色成員的任何使用者查詢。  
  
> [!NOTE]  
>  您在這個課程中建立的 Sales Employees by Territory 角色會限制成員只能瀏覽 (或查詢) 本身所屬銷售地區的銷售資料。 如果您將使用者新增為成員 Sales employees by Territory 角色同時也是在中建立的角色中的成員[第 12 課：建立角色](../analysis-services/lesson-11-create-roles.md)，您會獲得合併的權限。 當使用者是多個角色的成員時，針對每個角色定義的權限和資料列篩選器會累計。 也就是說，該使用者將具有大於角色組合所決定的權限。  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>若要建立 Sales Employees by Territory 使用者角色  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，按一下 [模型] 功能表，然後按一下 [角色]。  
  
2.  在 [角色管理員] 對話方塊中，按一下 [新增]。  
  
     具有「無」權限的新角色就會加入至清單中。  
  
3.  按一下新角色，然後在**名稱**資料行中，重新命名角色`Sales Employees by Territory`。  
  
4.  按一下 [權限] 資料行中的下拉式清單，然後選取 [讀取] 權限。  
  
5.  按一下 [成員] 索引標籤，然後按一下 [新增]。  
  
6.  在 [選取使用者或群組] 對話方塊中，於 [輸入要選取的物件名稱] 輸入您建立 Employee Security 資料表時使用的第一個範例使用者名稱。 按一下 [檢查名稱]，確認使用者名稱有效，然後按一下 [確定]。  
  
     重複這個步驟，加入您建立 Employee Security 資料表時使用的其他範例使用者名稱。  
  
7.  按一下 [資料列篩選器] 索引標籤。  
  
8.  針對`Employee Security`表格中，於**DAX 篩選** 欄中，輸入下列公式。  
  
     `=FALSE()`  
  
     完成建立公式時，按 ENTER。  
  
     這個公式會指定所有資料行都解析為 False 布林值條件；因此，Sales Employees by Territory 使用者角色的成員無法查詢 Employee Security 資料表的任何資料行。  
  
9. 針對 [Sales Territory] 資料表，輸入下列公式。  
  
     `='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 'Employee Security'[Login Id], USERNAME(), 'Employee Security'[Sales Territory Id], 'Sales Territory'[Sales Territory Id])`  
  
     完成建立公式時，按 ENTER。  
  
     在這個公式中，LOOKUPVALUE 函數會傳回 Employee Security[Sales Territory Id] 資料行的所有值，其中 Employee Security[Login Id] 與目前登入的 Windows 使用者名稱相同，而 Employee Security[Sales Territory Id] 與 Sales Territory[Sales Territory Id] 相同。  
  
     LOOKUPVALUE 所傳回的 Sales Territory ID 集會用來限至 Sales Territory 資料表中顯示的資料列。 只有資料列的 Sales Territory ID 落在 LOOKUPVALUE 函數所傳回的 ID 集之中的資料列才會顯示。  
  
10. 在 [角色管理員] 對話方塊中，按一下 [確定]。  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>測試 Sales Employees by Territory 使用者角色  
 在這項工作中，您將使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的 [在 Excel 中進行分析] 功能來測試 Sales Employees by Territory 使用者角色的效用。 您將指定其中一個加入至 Employee Security 資料表且做為角色成員的使用者名稱。 然後這個使用者名稱會做為 Excel 和模型之間所建立連接中的有效使用者名稱。  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>若要測試 Sales Employees by Territory 使用者角色  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[在 Excel 中進行分析]**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊的 [指定用於連接模型的使用者名稱或角色] 中，選取 [其他 Windows 使用者]，然後按一下 [瀏覽]。  
  
3.  在 [選取使用者或群組] 對話方塊中，於 [輸入要選取的物件名稱] 輸入您加入 Employee 資料表中的其中一個使用者名稱，然後按一下 [檢查名稱]。  
  
4.  按一下 [確定] 關閉 [選取使用者或群組] 對話方塊，然後按一下 [確定] 關閉 [在 Excel 中進行分析] 對話方塊。  
  
     Excel 將會開啟，並顯示一個新的活頁簿。 樞紐分析表會自動建立。 [樞紐分析表欄位清單] 包含新模型中大部分可用的資料欄位。  
  
     請注意，Employee Security 資料表不會在 [樞紐分析表欄位清單] 中顯示。 這是因為您在前一項工作中選擇了對用戶端工具隱藏這個資料表。  
  
5.  在 [樞紐分析表欄位] 清單中，於 [∑ Internet Sales] (量值) 中選取 [Internet Total Sales] 量值。 這個量值將會輸入 [值] 欄位中。  
  
6.  在 [樞紐分析表欄位] 清單中，從 [Sales Territory] 資料表選取 [Sales Territory Id] 資料行。 這個資料行將會輸入 [資料列標籤] 欄位中。  
  
     請注意，只會出現您所使用的有效使用者名稱所屬地區的網際網路銷售數字。 如果您從 Geography 資料表選取另一個資料行 (例如，City) 做為 [資料列標籤] 欄位，則只會顯示有效使用者所屬銷售地區中的城市。  
  
     這個使用者無法瀏覽或查詢本身所屬地區以外之地區的任何網際網路銷售資料，因為 Sales Employees by Territory 使用者角色中針對 Sales Territory 資料表所定義的資料列篩選器有效地保護了與其他銷售地區相關之所有資料的安全。  
  
## <a name="see-also"></a>另請參閱  
 [USERNAME 函式&#40;DAX&#41;](https://msdn.microsoft.com/library/hh230954.aspx)   
 [LOOKUPVALUE 函式&#40;DAX&#41;](https://msdn.microsoft.com/library/gg492170.aspx)   
 [CUSTOMDATA 函式&#40;DAX&#41;](https://msdn.microsoft.com/library/hh213140.aspx)  
  
  
