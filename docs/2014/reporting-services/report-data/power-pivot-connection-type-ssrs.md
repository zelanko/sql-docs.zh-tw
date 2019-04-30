---
title: PowerPivot 連接類型 (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a104c3c7-f118-4d02-9a0f-6859f1469d11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b391c7e76ab5feeeb6e355924349a578c446c882
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63218049"
---
# <a name="powerpivot-connection-type-ssrs"></a>PowerPivot 連接類型 (SSRS)
  您可以使用 SQL Server Analysis Services 資料處理延伸模組，從已在 SharePoint PowerPivot 圖庫中發行的 PowerPivot 活頁簿中擷取資料。  
  
 您可以使用本主題中的資訊來建置資料來源。 如需逐步指示，請參閱 <<c0> [ 加入及驗證資料連接或資料來源&#40;報表產生器及 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)。</c0>  
  
## <a name="prerequisites"></a>先決條件  
 您必須在 SharePoint 網站的 PowerPivot 圖庫中發行 PowerPivot 資料來源。  
  
 若要支援報表產生器與 PowerPivot 活頁簿的連接，您的工作站電腦上必須擁有 SQL Server 2008 R2 ADOMD.NET。 此用戶端程式庫隨 PowerPivot for Excel 一併安裝，但如果您使用沒有此應用程式的電腦，您必須下載並安裝 ADOMD.NET 從[SQL Server 2008 R2 功能套件](https://go.microsoft.com/fwlink/?LinkId=192565)。  
  
## <a name="data-source-type"></a>資料來源類型  
 請使用報表資料來源類型： **Microsoft SQL Server Analysis Services**。  
  
## <a name="connection-string"></a>連接字串  
 連接字串是在 SharePoint 中 PowerPivot 圖庫或其他程式庫，例如，發行的 PowerPivot 活頁簿的 URL http://contoso-srv/subsite/PowerPivotLibrary/ContosoSales.xlsx。  
  
## <a name="credentials"></a>認證  
 請指定存取 PowerPivot 活頁簿和 SharePoint 網站所需的認證，例如 Windows 驗證 (整合式安全性)。 如需詳細資訊，請參閱 <<c0> [ 資料連接、 資料來源和 Reporting Services 中的連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)或是[在 報表產生器中指定認證](../specify-credentials-in-report-builder.md)。  
  
## <a name="queries"></a>查詢  
 在您連接至 PowerPivot 資料來源之後，請使用 MDX 圖形化查詢來建立查詢，其方式是從基礎資料結構進行瀏覽及選取。 建立查詢之後，請執行查詢，於結果窗格中查看範例資料。  
  
 查詢設計工具會分析該查詢來決定資料集的欄位。 您也可以在 [報表資料] 窗格中手動編輯資料集欄位集合。 如需詳細資訊，請參閱[加入、編輯、重新整理報表資料窗格中的欄位 &#40;報表產生器及 SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)。  
  
## <a name="filters"></a>篩選  
 在 [篩選] 窗格中，請指定要從查詢結果中篩選出或包含在查詢結果中的維度和成員。  
  
## <a name="parameters"></a>參數  
 在 [篩選] 窗格中，選取篩選的 [參數] 選項，以便使用對應至篩選選取範圍的可用值來自動建立報表參數。  
  
## <a name="remarks"></a>備註  
 如果您從 PowerPivot 圖庫中的 PowerPivot 活頁簿開啟報表產生器，該報表就不會重新建立樞紐分析表、樞紐分析圖、交叉分析篩選器，以及來自 PowerPivot 活頁簿的其他配置和分析功能。 而是，空白報表會包括指向 PowerPivot 活頁簿中資料的預先設定資料來源。 根據您想要在報表中重新建立的交叉分析篩選器、篩選和資料表或圖表數目，設計以 PowerPivot 活頁簿為基礎的報表可能會相當費時耗力。 較佳的方法是分開想像報表資料的呈現方式與 PowerPivot 設計方式。  
  
 PowerPivot 活頁簿中的資料會進行高度壓縮，而針對報表從 PowerPivot 活頁簿中擷取的資料則不會進行壓縮。 您可以使用查詢設計工具來指定篩選和參數，以便將資料限制為報表所需的項目。  
  
 與連接至 Analysis Services Cube 不同的是，PowerPivot 模型沒有任何階層。 若要提供類似的功能給活頁簿中的相關交叉分析篩選器，您必須在報表中建立串聯參數。 如需詳細資訊，請參閱 [將串聯參數加入至報表 &#40;報表產生器及 SSRS&#41;](../report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)中建立的行動報表。  
  
 在某些情況下，您可能需要調整運算式，才能容納來自 PowerPivot 模型的基礎資料值。 若要將資料轉換成正確的資料類型，或是加入或移除彙總函式，您可能需要修改運算式。 例如，若要將資料類型從字串轉換成整數，請使用 `=CInt`。 發行報表之前，請務必確認報表顯示 PowerPivot 模型中資料的預期值。  
  
 只有在符合下列條件時，才會產生 PowerPivot 圖庫中報表的預覽影像：  
  
-   報表和提供資料的 PowerPivot 活頁簿必須一起儲存在相同的 PowerPivot 圖庫中。  
  
-   報表只包含 PowerPivot 資料來源中的 PowerPivot 資料。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services MDX 查詢設計工具使用者介面 &#40;報表產生器&#41;](../analysis-services-mdx-query-designer-user-interface-report-builder.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
