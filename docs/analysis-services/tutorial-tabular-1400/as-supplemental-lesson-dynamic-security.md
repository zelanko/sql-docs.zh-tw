---
title: Analysis Services 教學課程補充課程： 動態安全性 |Microsoft 文件
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: 15ff0eebd7cbbb0815544b18f0f042ef411a3657
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43084591"
---
# <a name="supplemental-lesson---dynamic-security"></a>補充課程 - 動態安全性

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在此補充課程中，您可以建立其他角色來實作動態安全性。 動態安全性提供以使用者目前登入的使用者名稱或登入識別碼為主的資料列層級安全性。 
  
若要實作動態安全性，您可以加入資料表至包含這些使用者可以連接至模型，並瀏覽模型物件和資料的使用者名稱。 使用本教學課程中您所建立的模型位於 Adventure Works; 的內容不過，若要完成這一課，您必須新增資料表，其中包含您自有網域中的使用者。 您不需要新增的使用者名稱的密碼。 若要建立 EmployeeSecurity 資料表，使用您自己的網域使用者的小型範例，您使用 [貼上] 功能中，貼上的 Excel 試算表中的員工資料。 在真實世界案例中，包含使用者名稱的資料表通常是來自實際資料庫的資料表做為資料來源;例如，實際的 DimEmployee 資料表。  
  
若要實作動態安全性，您可以使用兩個 DAX 函數︰ [USERNAME 函數 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)並[LOOKUPVALUE 函數 (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)。 這兩個函數是在新角色中定義，並且會套用至資料列篩選器公式。 藉由使用 LOOKUPVALUE 函式，此公式會指定 EmployeeSecurity 表中的值。 此公式接著將傳遞至 USERNAME 函式，其指定登入之使用者的使用者名稱的值屬於此角色。 之後使用者就只能瀏覽角色的資料列篩選器所指定的資料。 在此案例中，您指定的銷售員工只能瀏覽不是成員的銷售地區的網際網路銷售資料。  
  
例如此 Adventure Works 表格式模型案例專屬的工作就是這類工作，但不一定適用於真實案例。 每一項工作都包含描述工作目的的其他資訊。  
  
完成本課程的估計時間： **30 分鐘**  
  
## <a name="prerequisites"></a>先決條件  

本文補充課程是表格式模型化教學課程中，應該依序完成的一部分。 在執行本補充課程中的工作之前，您應已完成之前所有課程。  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>將 dimSalesTerritory 資料表加入至 AW Internet Sales 表格式模型專案  

若要實作此 Adventure Works 案例的動態安全性，您必須將額外兩個資料表加入至模型。 您新增的第一個資料表是來自相同 AdventureWorksDW 資料庫的 DimSalesTerritory （做為銷售地區）。 您稍後會套用到 SalesTerritory 資料表定義的登入的使用者可以瀏覽的特定資料的資料列篩選器。  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>若要加入 dimSalesTerritory 資料表  
  
1.  在表格式模型總管 中 >**資料來源**，以滑鼠右鍵按一下您的連線，然後按一下**匯入新資料表**。  

    如果出現 [模擬認證] 對話方塊，請輸入您在第 2 課＜加入資料＞中使用的模擬認證。
  
2.  在 導覽器中，選取**DimSalesTerritory**資料表，然後按一下**確定**。    
  
3.  在 [查詢編輯器] 中，按一下**DimSalesTerritory**查詢，然後再移除**SalesTerritoryAlternateKey**資料行。  
  
7.  按一下 **[匯入]**。  
  
    新的資料表加入至模型工作區。 然後，物件與來源 DimSalesTerritory 資料表中的資料會匯入 AW Internet Sales 表格式模型。  
  
9. 已成功匯入資料表之後，請按一下**關閉**。  

## <a name="add-a-table-with-user-name-data"></a>加入包含使用者名稱資料的資料表  

AdventureWorksDW 範例資料庫中的 DimEmployee 資料表包含來自 AdventureWorks 網域的使用者。 這些使用者名稱不存在於您自己的環境。 您必須在包含從您的組織中實際使用者 （至少三個） 的小型範例模型中建立資料表。 您接著將這些使用者做為成員加入新的角色。 您不需要密碼範例使用者名稱，但您需要實際的 Windows 使用者名稱從您自己的網域。  
  
#### <a name="to-add-an-employeesecurity-table"></a>若要新增 EmployeeSecurity 資料表  
  
1.  開啟 Microsoft Excel，並建立工作表。  
  
2.  複製下列資料表，包括標頭資料列，然後將它貼入工作表中。  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  名字、 姓氏和網域 \ 使用者名稱取代名稱與您的組織中三個使用者的登入識別碼。 針對 EmployeeId 1，顯示此使用者屬於一個以上的銷售領域置於前兩個資料列中，相同的使用者。 不，請保留 EmployeeId 和 SalesTerritoryId 欄位。  
  
4.  儲存為工作表**SampleEmployee**。  
  
5.  在工作表中，選取 包含員工資料，包括標頭的所有儲存格然後以滑鼠右鍵按一下選取的資料，然後按一下**複製**。  
  
6.  在 SSDT 中，按一下**編輯**功能表，然後再按一下**貼上**。  
  
    如果貼上會呈現灰色，按一下 模型設計師視窗中的任何資料表中的任何資料行，並再試一次。  
  
7.  在 **貼上預覽**對話方塊中，於**資料表名稱**，型別**EmployeeSecurity**。  
  
8.  在 **要貼上資料**，確認資料包含所有的使用者資料和從 SampleEmployee 工作表的標頭。  
  
9. 確認已核取 [使用第一個資料列作為資料行標頭]，然後按一下 [確定]。  
  
    建立新的資料表，名為 EmployeeSecurity 包含從 SampleEmployee 工作表複製的員工資料。  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>建立 FactInternetSales、 DimGeography 和 DimSalesTerritory 資料表之間的關聯性  

FactInternetSales、 DimGeography 和 DimSalesTerritory 資料表全都包含常用的資料行，SalesTerritoryId。 DimSalesTerritory 資料表中的 SalesTerritoryId 資料行包含不同的識別碼，每個銷售地區的值。  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a>建立 FactInternetSales、 DimGeography 和 DimSalesTerritory 資料表之間的關聯性  
  
1.  在圖表檢視中，在**DimGeography**資料表中，按一下，並保留**SalesTerritoryId**資料行，然後拖曳游標以**SalesTerritoryId** 中的資料行**DimSalesTerritory**資料表，然後再放開。  
  
2.  在**FactInternetSales**資料表中，按一下，並保留**SalesTerritoryId**資料行，然後拖曳游標以**SalesTerritoryId**中的資料行**DimSalesTerritory**資料表，然後再放開。  
  
    請注意此關聯性的 Active 屬性為 False，亦即非作用中。 在 FactInternetSales 資料表已經有另一個使用中關聯性。  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>隱藏 EmployeeSecurity 資料表從用戶端應用程式  

在這個工作中，您隱藏 EmployeeSecurity 資料表，使其不會出現在用戶端應用程式欄位清單。 請記住，隱藏資料表不會保護它。 使用者仍可查詢 EmployeeSecurity 資料表資料，如果他們知道方式。 若要保護 EmployeeSecurity 資料表資料，防止使用者查詢其中的任何資料，您可以套用篩選，以在稍後的工作。  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>若要隱藏 EmployeeSecurity 資料表，從用戶端應用程式  
  
-   在模型設計師的 [圖表檢視] 中，以滑鼠右鍵按一下 [Employee] 資料表標題，然後按一下 [在用戶端工具中隱藏]。  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>建立 Sales Employees by Territory 使用者角色  

在這個工作中，您可以建立使用者角色。 這個角色包含定義 DimSalesTerritory 資料表的資料列會對使用者顯示的資料列篩選器。 篩選條件則會套用至 DimSalesTerritory 相關的所有其他資料表的一對多關聯性方向中。 您也可以套用篩選條件，以防止任何使用者角色的成員可以查詢整個 EmployeeSecurity 資料表。  
  
> [!NOTE]  
> 您在這個課程中建立的 Sales Employees by Territory 角色會限制成員只能瀏覽 (或查詢) 本身所屬銷售地區的銷售資料。 如果您將使用者新增為成員 Sales employees by Territory 角色同時也是在中建立的角色中的成員[第 11 課： 建立角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)，您會獲得合併的權限。 當使用者是多個角色的成員時，針對每個角色定義的權限和資料列篩選器會累計。 也就是說，使用者會有更高的權限的角色組合所決定的。  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>若要建立 Sales Employees by Territory 使用者角色  
  
1.  在 SSDT 中，按一下**模型**功能表，然後再按一下**角色**。  
  
2.  在 **角色管理員**，按一下**新增**。  
  
    具有「無」權限的新角色就會加入至清單中。  
  
3.  按一下新角色，然後在**名稱**資料行中，重新命名角色**Sales Employees by Territory**。  
  
4.  按一下 [權限] 資料行中的下拉式清單，然後選取 [讀取] 權限。  
  
5.  按一下 **成員**索引標籤，然後再按一下**新增**。  
  
6.  在 **選取使用者或群組**對話方塊中，於**輸入要選取的物件名稱**，輸入您建立 EmployeeSecurity 資料表時使用的第一個範例使用者名稱。 按一下 [檢查名稱]，確認使用者名稱有效，然後按一下 [確定]。  
  
    重複此步驟中，新增的其他範例使用者名稱建立 EmployeeSecurity 資料表時使用。  
  
7.  按一下 [**資料列篩選器**] 索引標籤。  
  
8.  針對**EmployeeSecurity**表格中，於**DAX 篩選** 欄中，輸入下列公式：  
  
    ```
      =FALSE()  
    ```
  
    此公式指定所有資料行，解析為 false，則為 True 的條件。 Sales Employees 的成員可以不查詢 EmployeeSecurity 資料表的任何資料行 by Territory 使用者角色。  
  
9. 針對**DimSalesTerritory**資料表中，輸入下列公式：  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    在此公式中，LOOKUPVALUE 函數會傳回 DimEmployeeSecurity [SalesTerritoryId] 資料行，其中 EmployeeSecurity [LoginId] 等同於目前登入的 Windows 使用者名稱，而 EmployeeSecurity [SalesTerritoryId] 是所有的值與 DimSalesTerritory [SalesTerritoryId] 相同。  
  
    銷售領域識別碼 LOOKUPVALUE 所傳回的集合則用來限制 DimSalesTerritory 資料表中顯示的資料列中。 只有其中的資料列的 SalesTerritoryID 是 LOOKUPVALUE 函數所傳回的 Id 集合中的資料列會顯示。  
  
10. 在 [角色管理員] 中，按一下**Ok**。  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>測試 Sales Employees by Territory 使用者角色  

在這個工作中，您使用在分析在 SSDT 中的 Excel 功能測試的功效，Sales employees by Territory 使用者角色。 您可以指定其中一個您新增到 EmployeeSecurity 資料表，以及角色的成員身分的使用者名稱。 此使用者名稱，然後做為有效的使用者名稱，在 Excel 與模型之間所建立的連接。  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>若要測試 Sales Employees by Territory 使用者角色  
  
1.  在 SSDT 中，按一下**模型**功能表，然後再按一下**在 Excel 中的進行分析**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊的 [指定用於連接模型的使用者名稱或角色] 中，選取 [其他 Windows 使用者]，然後按一下 [瀏覽]。  
  
3.  在 **選取使用者或群組**對話方塊中，於**輸入物件名稱來選取**，輸入您包含在 EmployeeSecurity 資料表中，使用者名稱，然後按一下**檢查名稱**。  
  
4.  按一下 [確定] 關閉 [選取使用者或群組] 對話方塊，然後按一下 [確定] 關閉 [在 Excel 中進行分析] 對話方塊。  
  
    Excel 會開啟新的活頁簿。 自動建立樞紐分析表。 樞紐分析表欄位清單包含大部分的新模型中可用的資料欄位。  
  
    請注意 EmployeeSecurity 資料表不會顯示在樞紐分析表欄位清單。 您隱藏此資料表在先前工作中的用戶端工具中。  
  
5.  在 **欄位**清單中，於**∑ Internet Sales** （量值），選取**InternetTotalSales**量值。 這個量值輸入**值**欄位。  
  
6.  選取  **SalesTerritoryId**資料行**DimSalesTerritory**資料表。 這個資料行將會輸入**資料列標籤**欄位。  
  
    請注意，只會出現您所使用的有效使用者名稱所屬地區的網際網路銷售數字。 如果您選取另一個資料行，例如縣 （市） 作為資料列標籤 欄位中，DimGeography 資料表中會顯示在有效使用者所屬銷售地區的城市。  
    此使用者無法瀏覽或查詢不是其所屬的地區任何網際網路銷售資料。 這項限制是因為資料列篩選器針對 DimSalesTerritory 資料表定義，Sales Employees by Territory 使用者角色，在保護的其他銷售地區相關的所有資料。  
  
## <a name="see-also"></a>另請參閱  

[使用者名稱的函式 (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE 函式 (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA 函式 (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  
