---
title: "OLE DB 連線類型 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d00cb13b-e1c2-4300-a195-3da1430a2df1
caps.latest.revision: "8"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dcd1dc663a4e80845bcb725774bb8b591130c62c
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="ole-db-connection-type-ssrs"></a>OLE DB 連接類型 (SSRS)
  若要加入來自 OLE DB 資料提供者的資料，您必須具有以 OLE DB 類型之報表資料來源為基礎的資料集。 這個內建的資料來源類型是以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] OLE DB 資料處理延伸模組為基礎。  
  
 OLE DB 是一項資料存取技術，可讓用戶端連接至各種不同的資料提供者。 在您選取 OLE DB 資料來源類型之後，必須選取特定的資料提供者。 例如參數和認證這類功能的支援，是依據您選取的資料提供者而定。  
  
 您可以使用本主題中的資訊來建置資料來源。 如需逐步指示，請參閱 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 連接字串  
 OLE DB 資料處理延伸模組的連接字串會視您所要的資料提供者而定。 一般連接字串包含資料提供者支援的名稱/值組。 例如，下列連接字串便指 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 和 AdventureWorks 資料庫的 OLE DB 提供者：  
  
```  
Provider=SQLNCLI10.1;Data Source=server; Initial Catalog=AdventureWorks  
```  
  
 您使用的連接字串是依據您要連接的外部資料來源而定。 若要設定資料提供者所特有的連接字串屬性，請在 **[資料來源屬性]** 對話方塊的 **[一般]** 頁面上，按一下 **[建立]** 按鈕，以便開啟 **[連接屬性]** 對話方塊。 透過 **[資料連結屬性]** 對話方塊，設定延伸資料來源屬性。  
  
 如需更多連接字串的範例，請參閱 [報表產生器中的資料連接、資料來源及連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)。  
  
  
##  <a name="Credentials"></a> 認證  
 需要有認證才能夠執行報表、於本機預覽報表並且從報表伺服器預覽報表。  
  
 發行報表之後，您可能需要變更資料來源的認證，如此當報表在報表伺服器上執行時，擷取資料的權限就會是有效的。  
  
 如需詳細資訊，請參閱[資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 或[在報表產生器中指定認證](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
###### <a name="special-characters-in-a-password"></a>密碼中的特殊字元  
 如果您設定 OLE DB 資料來源來提示輸入密碼或是將密碼包含在連接字串中，則當使用者輸入含有特殊字元 (如標點符號) 的密碼時，某些基礎資料來源驅動程式將無法驗證這些特殊字元。 當您處理報表時，訊息「不是有效密碼」可能會指出此問題。  
  
> [!NOTE]  
>  建議您不要在連接字串中加入登入資訊，例如密碼。 報表產生器會在 **[資料來源]** 對話方塊中提供另一個索引標籤，您可以使用此索引標籤來輸入認證。  
  
  
##  <a name="Parameters"></a> 參數  
 有些 OLE DB 提供者支援未具名參數，而不支援具名參數。 參數是使用查詢中的預留位置依據位置傳遞。 預留位置字元是由資料提供者支援的語法決定。  
  
  
##  <a name="Remarks"></a> 備註  
 OLEDB 是一項原生技術，用於建立特定資料來源的資料提供者。 OLEDB 是以 COM (元件物件模型) 介面為基礎。 OLEDB 是比 ODBC 更新的技術，但是比 ADO.NET 資料提供者更早出現。 OLEDB 資料提供者會在作業系統中註冊，就像其他 COM 元件一般。 OLEDB 資料提供者可從 Microsoft 和協力廠商取得。 Microsoft 同時提供 MSDASQL，這是橋接與 ODBC 驅動程式之通訊的 OLEDB 資料提供者。 如需詳細資訊，請參閱 [ODBC 連線類型 &#40;SSRS&#41;](../../reporting-services/report-data/odbc-connection-type-ssrs.md)。  
  
 若要成功擷取您想要的資料，您必須提供資料提供者支援的查詢語法。 參數支援會因資料提供者而異。 如需詳細資訊，請參閱所選取資料提供者的特定主題。 例如：  
  
-   [Analysis Services OLE DB 提供者 &#40;Analysis Services - 多維度資料&#41;](http://msdn.microsoft.com/library/cdeecd50-1d91-4162-a4a2-01c7799b02a8)  
  
-   [使用 .NET Framework Data Provider for Oracle](http://go.microsoft.com/fwlink/?LinkId=112314)  
  
-   [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
 如需特定 OLE DB 資料提供者的詳細資訊，請參閱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
  
##  <a name="HowTo"></a> 如何主題  
 本節包含使用資料連接、資料來源與資料集的逐步指示。  
  
 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [將篩選加入資料集中 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 相關章節  
 本文件集的這些章節會提供報表資料的深入概念性資訊，以及如何定義、自訂和使用與報表資料相關組件的程序資訊。  
  
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 提供存取報表資料的概觀。  
  
 [報表產生器中的資料連接、資料來源及連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 提供資料連接與資料來源的相關資訊。  
  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供內嵌與共用資料集的相關資訊。  
  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 提供查詢所產生之資料集欄位集合的相關資訊。  
  
 《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書》](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
 提供支援每一個資料延伸模組之平台與版本的深入資訊。  
  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
