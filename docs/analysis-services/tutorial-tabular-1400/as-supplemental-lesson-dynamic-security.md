---
title: Analysis Services 教學課程，補充課程： 動態安全性 |Microsoft 文件
description: 描述如何使用動態安全性，Analysis Services 教學課程中使用資料列篩選。
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: ffd58456ee40741792ac7ce409c97e064a92ba43
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="supplemental-lesson---dynamic-security"></a>補充課程-動態安全性

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這個補充課程中，您可以建立實作動態安全性的其他角色。 動態安全性提供以使用者目前登入的使用者名稱或登入識別碼為主的資料列層級安全性。 
  
若要實作動態安全性，您可以加入資料表至包含這些使用者可以連接到模型並瀏覽模型物件和資料的使用者名稱。 您使用本教學課程所建立的模型位於 Adventure Works; 的內容不過，若要完成這一課，您必須加入資料表，包含從您自己的網域使用者。 您不需要加入的使用者名稱密碼。 若要建立 EmployeeSecurity 資料表中，從您自己的網域使用者的一小部分的範例，您使用貼上功能中，貼上的 Excel 試算表的員工資料。 在真實世界案例中，包含使用者名稱的資料表一般會實際的資料庫中的資料表做為資料來源;例如，實際的 DimEmployee 資料表。  
  
若要實作動態安全性，您可以使用兩個 DAX 函數： [USERNAME 函數 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)和[LOOKUPVALUE 函數 (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)。 這兩個函數是在新角色中定義，並且會套用至資料列篩選器公式。 使用 LOOKUPVALUE 函數，此公式會指定 EmployeeSecurity 表中的值。 公式然後傳遞至使用者名稱函式，指定登入之使用者的使用者名稱的值屬於此角色。 之後使用者就只能瀏覽角色的資料列篩選器所指定的資料。 在此案例中，您指定的銷售員工只能瀏覽網際網路銷售地區都是成員的銷售資料。  
  
例如此 Adventure Works 表格式模型案例專屬的工作就是這類工作，但不一定適用於真實案例。 每一項工作都包含描述工作目的的其他資訊。  
  
完成本課程的估計時間： **30 分鐘**  
  
## <a name="prerequisites"></a>필수 구성 요소  

本文補充課程是表格式模型化教學課程中，應該依序完成的一部分。 在執行本補充課程中的工作之前，您應已完成之前所有課程。  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>將 dimSalesTerritory 資料表加入至 AW Internet Sales 表格式模型專案  

若要實作此 Adventure Works 案例的動態安全性，您必須將兩個其他資料表加入至模型。 您加入的第一個資料表是來自相同 AdventureWorksDW 資料庫的 DimSalesTerritory （做為銷售地區）。 您稍後會將資料列篩選器套用至 SalesTerritory 資料表定義登入的使用者可以瀏覽特定的資料。  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>若要加入 dimSalesTerritory 資料表  
  
1.  在表格式模型總管 >**資料來源**，以滑鼠右鍵按一下您的連線，然後按一下**匯入新資料表**。  

    如果出現 [模擬認證] 對話方塊，請輸入您在第 2 課＜加入資料＞中使用的模擬認證。
  
2.  在 導覽器中，選取  **DimSalesTerritory**資料表，然後按一下 **確定**。    
  
3.  在 [查詢編輯器] 中，按一下**DimSalesTerritory**查詢，然後再移除 **[salesterritoryalternatekey]** 資料行。  
  
7.  **가져오기**를 클릭합니다.  
  
    新的資料表加入至模型工作空間。 物件和資料從來源 DimSalesTerritory 資料表接著會匯入 AW Internet Sales 表格式模型中。  
  
9. 已成功匯入資料表之後，請按一下**關閉**。  

## <a name="add-a-table-with-user-name-data"></a>加入包含使用者名稱資料的資料表  

AdventureWorksDW 範例資料庫中的 DimEmployee 資料表包含來自 AdventureWorks 網域的使用者。 這些使用者名稱不存在於您自己的環境。 您必須建立資料表，其中包含從您的組織中實際使用者 （至少三個） 的小型範例模型中。 您再將這些使用者為成員加入新的角色。 您不需要密碼的使用者名稱，但您需要實際的 Windows 使用者名稱從您自己的網域。  
  
#### <a name="to-add-an-employeesecurity-table"></a>若要加入 EmployeeSecurity 資料表  
  
1.  開啟 Microsoft Excel，建立工作表。  
  
2.  複製下列資料表，包括標頭資料列，然後將它貼入工作表中。  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  名字、 姓氏和 domain\username 取代名稱與您組織中的三個使用者的登入識別碼。 放入寄不相同的使用者在前兩個資料列中，EmployeeId 1，顯示此使用者屬於多個銷售領域。 EmployeeId 和 SalesTerritoryId 欄位保持不變。  
  
4.  做為工作表儲存**SampleEmployee**。  
  
5.  在表中，選取包含員工資料，包括標頭，所有資料格，然後以滑鼠右鍵按一下選取的資料，然後按一下**複製**。  
  
6.  在 SSDT 中，按一下 **編輯**功能表，然後再按一下**貼上**。  
  
    如果貼上呈現灰色時，按一下模型設計師視窗中的任何資料表中的任何資料行，並再試一次。  
  
7.  在**貼上預覽**對話方塊中，於**資料表名稱**，型別**EmployeeSecurity**。  
  
8.  在**要貼上資料**，確認資料包含所有的使用者資料和 SampleEmployee 工作表中的標頭。  
  
9. 確認已核取 [使用第一個資料列作為資料行標頭]，然後按一下 [確定]。  
  
    建立新的資料表，名為 EmployeeSecurity SampleEmployee 工作表複製的員工資料。  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>FactInternetSales、 DimGeography 和 DimSalesTerritory 資料表之間建立關聯性  

所有 FactInternetSales、 DimGeography 和 DimSalesTerritory 資料表包含常用的資料行，SalesTerritoryId。 SalesTerritoryId 中的資料行 DimSalesTerritory 資料表包含以每個銷售地區不同的識別碼值。  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a>若要建立 DimGeography，FactInternetSales DimSalesTerritory 資料表之間的關聯性  
  
1.  在圖表檢視中，在**DimGeography**資料表，按一下並按住**SalesTerritoryId**資料行，然後拖曳游標以**SalesTerritoryId**中的資料行**DimSalesTerritory**資料表，然後再放開。  
  
2.  在**FactInternetSales**資料表，按一下並按住**SalesTerritoryId**資料行，然後拖曳游標以**SalesTerritoryId**中的資料行**DimSalesTerritory**資料表，然後再放開。  
  
    請注意此關聯性的作用中 屬性為 False，亦即非使用中。 FactInternetSales 資料表已經有另一個使用中關聯性。  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>隱藏 EmployeeSecurity 表格，從用戶端應用程式  

在這項工作，您隱藏 EmployeeSecurity 資料表，使其不會出現在用戶端應用程式欄位清單中。 請注意，隱藏資料表不會保護其安全。 如果使用者知道，使用者仍然可以查詢 EmployeeSecurity 資料表資料方式。 若要保護 EmployeeSecurity 資料表資料，防止使用者查詢其中任何資料，您套用篩選，以在稍後的工作。  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>若要隱藏 EmployeeSecurity 表格，從用戶端應用程式  
  
-   在模型設計師的 [圖表檢視] 中，以滑鼠右鍵按一下 [Employee] 資料表標題，然後按一下 [在用戶端工具中隱藏]。  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>建立 Sales Employees by Territory 使用者角色  

在這項工作，您可以建立使用者角色。 這個角色包含定義 DimSalesTerritory 資料表的哪些資料列會對使用者顯示的資料列篩選。 然後套用篩選到 DimSalesTerritory 與相關的所有其他資料表的一對多關聯性方向。 您也可以套用篩選器，可保護整份 EmployeeSecurity 資料表進行任何使用者角色的成員可以查詢。  
  
> [!NOTE]  
> 您在這個課程中建立的 Sales Employees by Territory 角色會限制成員只能瀏覽 (或查詢) 本身所屬銷售地區的銷售資料。 如果您將使用者加入成為成員 Sales Employees by Territory 角色同時存在於中角色的成員建立時在[第 11 課： 建立角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)，取得權限的組合。 當使用者是多個角色的成員時，針對每個角色定義的權限和資料列篩選器會累計。 也就是說，使用者會有更高的權限角色組合所決定的。  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>若要建立 Sales Employees by Territory 使用者角色  
  
1.  在 SSDT 中，按一下 **模型**功能表，然後再按一下**角色**。  
  
2.  在**角色管理員**，按一下 **新增**。  
  
    具有「無」權限的新角色就會加入至清單中。  
  
3.  按一下新角色，然後在**名稱**資料行中，若要將角色重新命名**Sales Employees by Territory**。  
  
4.  按一下 [權限] 資料行中的下拉式清單，然後選取 [讀取] 權限。  
  
5.  按一下**成員**索引標籤，然後再按一下**新增**。  
  
6.  在**選取使用者或群組**對話方塊中，於**輸入物件名稱來選取**，輸入您建立 EmployeeSecurity 資料表時使用的第一個範例使用者名稱。 按一下 [檢查名稱]，確認使用者名稱有效，然後按一下 [確定]。  
  
    重複此步驟中，加入的其他範例使用者名稱建立 EmployeeSecurity 資料表時所使用。  
  
7.  按一下**資料列篩選器** 索引標籤。  
  
8.  如**EmployeeSecurity**表格中，於**DAX 篩選**資料行中，輸入下列公式：  
  
    ```
      =FALSE()  
    ```
  
    此公式會指定所有資料行解析為 false，則為 True 的條件。 Sales Employees 的成員可以查詢 EmployeeSecurity 資料表沒有資料行 by Territory 使用者角色。  
  
9. 如**DimSalesTerritory**資料表中，輸入下列公式：  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    在此公式中，LOOKUPVALUE 函數會傳回所有 DimEmployeeSecurity [SalesTerritoryId] 資料行，其中 EmployeeSecurity [LoginId] 等同於目前登入的 Windows 使用者名稱，而 EmployeeSecurity [SalesTerritoryId] 是 DimSalesTerritory [SalesTerritoryId] 相同的值。  
  
    銷售領域識別碼 LOOKUPVALUE 所傳回的集合然後用來限制顯示 DimSalesTerritory 資料表中的資料列。 只有其中資料列 SalesTerritoryID 是 LOOKUPVALUE 函數所傳回的 Id 集內的資料列會顯示。  
  
10. 在 [角色管理員] 中，按一下**確定**。  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>測試 Sales Employees by Territory 使用者角色  

在這個工作中，您使用中進行分析 在 SSDT 中的 Excel 功能來測試效率的 Sales Employees by Territory 使用者角色。 您可以指定一個您新增到 EmployeeSecurity 資料表以及角色的成員身分的使用者名稱。 建立 Excel 與模型之間的連接的有效使用者名稱再使用這個使用者名稱。  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>若要測試 Sales Employees by Territory 使用者角色  
  
1.  在 SSDT 中，按一下 **模型**功能表，然後再按一下**在 Excel 中的進行分析**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊的 [指定用於連接模型的使用者名稱或角色] 中，選取 [其他 Windows 使用者]，然後按一下 [瀏覽]。  
  
3.  在**選取使用者或群組**對話方塊中，於**輸入物件名稱來選取**，輸入您在 EmployeeSecurity 資料表中，包含使用者名稱，然後按一下**檢查名稱**。  
  
4.  按一下 [確定] 關閉 [選取使用者或群組] 對話方塊，然後按一下 [確定] 關閉 [在 Excel 中進行分析] 對話方塊。  
  
    Excel 會開啟新的活頁簿。 自動建立樞紐分析表。 樞紐分析表欄位清單包含大部分的新模型中可用的資料欄位。  
  
    請注意 EmployeeSecurity 資料表不是在樞紐分析表欄位清單中看到。 隱藏這個資料表，在先前工作中的用戶端工具中。  
  
5.  在**欄位**清單中， **∑ Internet Sales** （量值），選取**InternetTotalSales**量值。 量值輸入**值**欄位。  
  
6.  選取**SalesTerritoryId**資料行從**DimSalesTerritory**資料表。 資料行輸入到**資料列標籤**欄位。  
  
    請注意，只會出現您所使用的有效使用者名稱所屬地區的網際網路銷售數字。 如果您選取另一個資料行，例如縣 （市） 從 DimGeography 資料表作為資料列標籤 欄位中，會顯示只能在有效使用者所屬銷售地區的城市。  
    此使用者無法瀏覽或查詢一其所屬的領域的任何網際網路銷售資料。 這項限制是因為資料列篩選器定義的 DimSalesTerritory 表格中的 Sales Employees by Territory 使用者角色，可保護的其他銷售地區相關的所有資料的資料。  
  
## <a name="see-also"></a>另請參閱  

[USERNAME 函數 (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE 函數 (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA 函數 (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  
