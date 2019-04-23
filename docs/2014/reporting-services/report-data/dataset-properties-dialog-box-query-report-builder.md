---
title: 資料集屬性對話方塊、查詢 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10024"
ms.assetid: 75432318-0b00-4797-917c-0a2e74f9d951
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8a74bac81874eaeeecd9b9abcdcbfee27e07909c
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59967146"
---
# <a name="dataset-properties-dialog-box-query-report-builder"></a>資料集屬性對話方塊、查詢 (報表產生器)
  選取 **[資料集屬性]** 對話方塊上的 **[查詢]** ，從報表伺服器選擇共用資料集或是建立內嵌資料集。 如果是內嵌資料集，您必須選擇資料來源並建立查詢。  
  
 **[資料集屬性]** 對話方塊包含下列項目：  
  
-   [資料集屬性對話方塊、參數 &#40;報表產生器&#41;](../dataset-properties-dialog-box-parameters-report-builder.md)  
  
-   [資料集屬性對話方塊、欄位 &#40;報表產生器&#41;](../dataset-properties-dialog-box-fields-report-builder.md)  
  
-   [資料集屬性對話方塊、選項 &#40;報表產生器&#41;](dataset-properties-dialog-box-options-report-builder.md)  
  
-   [資料集屬性對話方塊、篩選 &#40;報表產生器&#41;](../dataset-properties-dialog-box-filters-report-builder.md)  
  
 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>選項。  
 **名稱**  
 輸入資料集的名稱。 此名稱不可以與報表中任何資料區域或群組的名稱相同。  
  
 **使用共用資料集**  
 選取這個選項可以從報表伺服器使用預先定義的資料集。  
  
 **瀏覽**  
 瀏覽到報表伺服器或 SharePoint 網站上的資料夾，並選取共用資料集 (.rsd)。  
  
 **在報表中使用內嵌資料集**  
 選取此選項，即可建立僅供這份報表使用的資料集。  
  
 **資料來源**  
 選取要做為資料集基礎的資料來源。 若要建立新的資料來源，按一下 **[新增]**。  
  
 **查詢類型**  
 選取資料集使用的命令或查詢類型。 選取 **[文字]** 來執行查詢，以便從資料庫中擷取資料。 選取 **[資料表]** 即可使用 **的** [TableDirect] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能來選取資料表中的所有欄位。 選取 **[預存程序]** 即可依名稱執行預存程序。 依預設，會選取 **[文字]** ，這適用於大多數的查詢。 若要編輯選取的資料來源查詢，按一下 **[查詢設計工具]**。  
  
> [!NOTE]  
>  並非所有的查詢類型都受到所有資料來源的支援。 例如， **[資料表]** 只受到 **[OLE DB]** 和 **[ODBC]** 資料來源類型的支援。  
  
 **[資料集屬性]**  
 此選項會在選擇 [文字] 命令類型選項時出現。 鍵入查詢，或按一下 [匯入] 來匯入已存在的查詢。 請按一下 **「運算式」** (*fx*) 按鈕來編輯運算式。  
  
> [!NOTE]  
>  如果您使用查詢設計工具來建立查詢，則查詢的文字會顯示在此方塊中。  
  
 **資料表名稱**  
 輸入您想要當做資料集使用之資料表的名稱。 此選項會在您選取 **[資料表]** 時出現。  
  
 **選取或輸入預存程序名稱**  
 輸入或選擇您要使用之預存程序的名稱。 請按一下 **運算式** (*fx*) 按鈕來編輯運算式。 此選項會在選擇 [預存程序] 命令類型選項時出現。  
  
 **逾時 (以秒為單位)**  
 輸入查詢逾時之前的秒數。預設值是 30 秒。 **[逾時]** 的值必須是空白或大於零。 如果是空白，則查詢不會逾時。  
  
 **重新整理欄位**  
 執行查詢命令，以更新 [資料集屬性對話方塊、欄位](../dataset-properties-dialog-box-fields-report-builder.md) 頁面上的欄位清單。  
  
## <a name="see-also"></a>另請參閱  
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-datasets-ssrs.md)   
 [對話方塊、窗格和精靈的報表產生器說明](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [查詢設計工具 &#40;報表產生器&#41;](../query-designers-report-builder.md)  
  
  
