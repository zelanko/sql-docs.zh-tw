---
title: "從資料採礦模型擷取資料 (DMX) (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retrieving report data
- datasets [Reporting Services], with DMX queries
- datasets [Reporting Services], Analysis Services
- queries [Reporting Services], data mining prediction
ms.assetid: d9cd3624-1594-4707-8887-55437dd7e07c
caps.latest.revision: "19"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 41e62ecb44bec44652262f47fc7635e5c613e233
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="retrieve-data-from-a-data-mining-model-dmx-ssrs"></a>從資料採礦模型擷取資料 (DMX) (SSRS)
  若要在報表中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料採礦模型內的資料，您必須定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源，並建立一或多個報表資料集。 當您建立資料來源定義時，您必須指定連接字串和認證，好讓您可以從用戶端電腦存取資料來源。  
  
 您可以建立內嵌資料來源定義供單一報表使用，或是建立共用資料來源定義供多個報表使用。 本主題的程序描述如何建立內嵌資料來源。 如需共用資料來源的詳細資訊，請參閱[內嵌和共用資料連線或資料來源 &#40;報表產生器及 SSRS&#41;](http://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56) 和[建立、修改及刪除共用資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)。  
  
 在您建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源之後，可以建立一或多個資料集。 您可針對每一個資料集使用資料採礦預測運算式 (DMX) 查詢設計工具，以建立一個指定欄位集合的 DMX 查詢。 如需詳細資訊，請參閱 [Analysis Services MDX 查詢設計工具使用者介面](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)。  
  
 在您建立資料集之後，該資料集的名稱會出現在 [報表資料] 窗格中，當做其資料來源底下的一個節點。  
  
 發行報表之後，您可能需要變更資料來源的認證，如此當報表在報表伺服器上執行時，擷取資料的權限就會是有效的。  
  
### <a name="to-create-an-embedded-microsoft-sql-server-analysis-services-data-source"></a>建立內嵌 Microsoft SQL Server Analysis Services 資料來源  
  
1.  在 [報表資料] 窗格的工具列上，按一下 **[新增]**，然後按一下 **[資料來源]**。  
  
2.  在 [資料來源屬性] 對話方塊中，於 [名稱] 文字方塊內鍵入名稱，或是接受預設名稱。  
  
3.  確認 [內嵌連線] 已選取。  
  
4.  從 [類型] 下拉式清單中，選取 [Microsoft SQL Server Analysis Services]。  
  
5.  指定與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源搭配使用的連接字串。  
  
     請洽詢資料庫管理員，以取得用來連接資料來源的連接資訊和認證。 下列連接字串範例會在本機用戶端上指定範例 [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] 資料庫。  
  
    ```  
    Data Source=localhost;Initial Catalog=AdventureWorksDW2012  
    ```  
  
6.  按一下 **[認證]**。  
  
     設定用來連接資料來源的認證。 如需詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)。  
  
    > [!NOTE]  
    >  若要測試資料來源連線，請按一下 [編輯]。 在 [連接屬性] 對話方塊中，按一下 [測試連線]。 如果測試成功，您將會看到「連接測試成功」的通知訊息。 如果測試失敗，您將會看到一個警告訊息，其中包含測試未能成功之原因的相關資訊。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     資料來源會出現在 [報表資料] 窗格中。  
  
### <a name="to-create-a-dataset-for-a-microsoft-sql-server-analysis-services"></a>若要為 Microsoft SQL Server Analysis Services 建立資料集  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源的資料來源名稱，然後按一下 [新增資料集]。  
  
2.  在 [資料集屬性] 對話方塊中，於 [名稱] 文字方塊內鍵入名稱。  
  
3.  在 [資料來源] 方塊中，確認該名稱為連線到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源的資料來源名稱。  
  
4.  按一下 [查詢設計工具]，開啟圖形化查詢設計工具來以互動方式建立查詢。 如果查詢設計工具以 MDX 模式開啟，請按一下工具列上的 [命令類型 DMX] (![變更為 DMX 查詢語言檢視](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "變更為 DMX 查詢語言檢視"))，切換到資料採礦查詢設計工具。 如需詳細資訊，請參閱 [Analysis Services MDX 查詢設計工具使用者介面](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)。  
  
     或者，若要從其他報表匯入現有的 DMX 查詢，請按一下 [匯入]，然後巡覽至包含 DMX 查詢的 .rdl 檔案。 不支援從 .dmx 檔案匯入查詢。  
  
5.  在您建立及執行查詢來查看範例結果之後，請按一下 [確定]。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     資料集和它的欄位集合會出現在 [報表資料] 窗格的資料來源節點底下。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Connection Type for DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
