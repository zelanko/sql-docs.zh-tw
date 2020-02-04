---
title: 新增、變更或刪除報表參數 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d44a8e0a-10cf-4502-9391-09743ffc9bad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: eb0d29f62a3751f0b8b6acd1c33c7b7f7eb10ff2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "65582064"
---
# <a name="add-change-or-delete-a-report-parameter-report-builder-and-ssrs"></a>加入、變更或刪除報表參數 (報表產生器及 SSRS)
  報表參數可讓您選擇報表資料、將相關的報表連接在一起，以及變更報表呈現方式。 您可以提供預設值和可用值的清單，而且使用者可以變更選取範圍。  
  
 在您發行報表之後，可以在報表伺服器上變更報表參數的預設值、可用值，以及其他屬性。 您可以建立連結報表來提供多組預設參數值。 如需詳細資訊，請參閱 MSDN 上的 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)類型之報表資料來源為基礎的資料集。  
  
 本文是關於將報表參數新增至 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]或報表設計師的分頁報表。 您也可以將報表參數新增至 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]中的行動報表。 如需詳細資訊，請參閱 [使用 SQL Server 行動報表發行工具建立行動報表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-or-edit-a-report-parameter"></a>若要加入或編輯報表參數  
  
1.  在 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 內，[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或報表設計師中的 [報表資料]  窗格中，以滑鼠右鍵按一下 [參數]  節點，然後按一下 [新增參數]  。 **[報表參數屬性]** 對話方塊隨即開啟。  
  
2.  在 **[名稱]** 中，輸入參數的名稱或接受預設的名稱。  
  
3.  在 **[提示]** 中，輸入使用者執行報表時，在參數文字方塊旁邊顯示的文字。  
  
4.  在 **[資料類型]** 中，選取參數值的資料類型。  
  
5.  如果參數可以包含空白值，請選取 **[允許空白值]** 。  
  
6.  如果參數可以包含 Null 值，請選取 **[允許 Null 值]** 。  
  
7.  若要允許使用者針對參數選取多個值，請選取 **[允許多個值]** 。  
  
8.  設定可見性選項。  
  
    -   若要在報表頂端的工具列上顯示此參數，請選取 **[可見]** 。  
  
    -   若要隱藏此參數而不顯示在工具列上，請選取 **[隱藏]** 。  
  
    -   若要隱藏此參數並且防止任何人在發行報表之後於報表伺服器上修改此參數，請選取 **[內部]** 。 然後，報表參數就只能在報表定義中檢視。 若要使用此選項，您必須設定預設值或允許參數接受 Null 值。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-report-parameter"></a>若要刪除報表參數  
  
1.  在 **[報表資料]** 窗格中，展開 **[參數]** 節點。  
  
2.  以滑鼠右鍵按一下報表參數，然後按一下 **[刪除]** 。  
  
## <a name="see-also"></a>另請參閱  
 [為報表參數加入、變更或刪除可用的值 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md)   
 [為報表參數新增、變更或刪除預設值 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-default-values-for-a-report-parameter.md)   
 [變更報表參數的順序 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [將串聯參數加入至報表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教學課程：將參數新增至報表 &#40;報表產生器&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [參數集合參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [將多值參數加入至報表](../../reporting-services/report-design/add-a-multi-value-parameter-to-a-report.md)  
  
  
