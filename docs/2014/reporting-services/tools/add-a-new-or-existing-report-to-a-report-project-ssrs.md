---
title: 將新的或現有的報表新增至報表專案 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bd6b3cc87757a8d0edc9067bd2f8f0911ccef238
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66100473"
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>將新的或現有的報表加入報表專案 (SSRS)
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，您可以使用 [報表精靈] 或將新的空白報表加入至專案，藉以加入新的報表。 您也可以加入現有的報表。 新增報表之後，您就可以看到報表名稱列在專案的 [報表]  資料夾下。  
  
> [!NOTE]  
>  若要預覽具有現有資料來源的報表，您必須擁有報表撰寫用戶端之資料來源的權限。 如需詳細資訊，請參閱[建立內嵌或共用資料來源 &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)。  
  
 在您加入報表之後，就可以定義資料來源和資料集，以及設計報表配置。 若要開始使用，請參閱[建立基本資料表報表 &#40;SSRS 教學課程&#41;](../create-a-basic-table-report-ssrs-tutorial.md) 或[資料表 &#40;報表產生器及 SSRS&#41;](../report-design/tables-report-builder-and-ssrs.md)。  
  
### <a name="to-add-a-new-report-using-the-report-wizard"></a>使用報表精靈來加入新的報表  
  
1.  在方案總管中，以滑鼠右鍵按一下 [報表] 資料夾，然後按一下 [新增新的報表]  。 [報表精靈]  對話方塊隨即開啟。  
  
     這個精靈會逐步引導您建立資料來源、建立含有查詢的資料集、定義群組、指定配置、選擇含有色彩和字型的樣式，以及建立報表。 步驟包括：  
  
    -   **選取資料來源。** 建立報表的第一個步驟是定義資料來源。 [報表精靈] 提供報表專案中所有共用資料來源的清單，也提供建立新資料來源的選項。  
  
    -   **設計查詢。** 下一個步驟是設計查詢。 您可以輸入查詢字串、使用查詢設計工具來建立它，或從其他報表匯入查詢。 如需查詢設計工具的相關資訊，請參閱 [Reporting Services 查詢設計工具](../reporting-services-query-designers.md)。  
  
    -   **選擇報表類型。** 下一個步驟是選取您要的報表類型。 您可以選擇表格式或矩陣報表。 表格式報表有固定的資料行數目。 矩陣 (或稱為交叉資料表) 報表會根據查詢的結果，而有不同的資料行數目。 對應報表會針對地理背景顯示分析。  
  
    -   **選擇樣式。** 下一個步驟是使用樣式範本，將樣式套用至報表。 請選取範本，以便將字型、色彩和框線等樣式套用至報表。 報表設計師提供六種樣式範本：Slate、Forest、Corporate、Bold、Ocean 和 Generic。 您也可以加入其他樣式範本。  
  
        > [!NOTE]  
        >  您可以\\藉由編輯 \Program Files\Microsoft Visual Studio 10.0 \ Common7\IDE\PrivateAssemblies\Business 情報 Wizards\Reports\Styles<lang\>資料夾中的 styletemplates.xml，來改變現有的範本或加入新範本，其中\<lang> 是您所使用的語言（例如，如果您使用的是英文版[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，則資料夾名稱為 "EN"）。 此資料夾位於安裝報表設計師的電腦上。 StyleTemplates.xml 檔案有兩個副本。 若要修改透過 [報表精靈] 套用的樣式，請編輯針對您使用的語言所建立之資料夾內的檔案。  
  
    -   **為報表命名。**  ：最後一個步驟是為報表命名，並確認報表中將要包含的欄位。 所有步驟都完成之後，報表設計師會建立報表，並將其加入報表伺服器專案。  
  
### <a name="to-add-a-new-blank-report"></a>加入新的空白報表  
  
1.  在 [專案]**** 功能表中，按一下 [新增項目]****。  
  
2.  在 [範本]**** 中，按一下 [報表]****。  
  
3.  按一下 **[新增]** 。  
  
     新的空白報表就會加入至專案並且顯示在設計介面上。  
  
### <a name="to-add-an-existing-report"></a>加入現有的報表  
  
1.  從 [**專案**] 功能表中，依序按一下 [**加入**] 和 [**現有專案**]。  
  
2.  巡覽至 .rdl 檔的位置、選取該檔案，然後按一下 [新增]****。  
  
     報表就會新增至 [報表]**** 資料夾底下的專案。 當您關閉並重新開啟專案時，這些報表就會按照字母順序排序。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 教學課程 &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  
