---
title: 建立連結的報表 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: df16c043688de82a549ec506ece457730626dda1
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50029057"
---
# <a name="create-a-linked-report"></a>建立連結報表
  連結報表是提供現有報表之存取點的報表伺服器項目。 它在概念上類似於您用來執行程式或開啟檔案的程式捷徑。  
  
 連結報表是從現有的報表衍生，並保留原始的報表定義。 連結報表一律繼承原始報表的報表配置與資料來源屬性。 其他所有屬性與設定可以和原始報表不同，包括安全性、參數、位置、訂閱，以及排程。  
  
 您想要建立現有報表的其他版本時，可以建立連結報表。 例如，您可以使用單一區域銷售報表，來建立您所有銷售地區的區域特定報表。  
  
 雖然連結報表通常是以參數化報表為基礎，但參數化報表並不是必要的。 每當您想要以不同的設定部署現有的報表時，都可以建立連結報表。  
  
### <a name="to-create-a-linked-report"></a>若要建立連結報表  
  
1.  在報表管理員中，導覽至包含您要連結之報表的資料夾，然後開啟選項功能表。您可以按一下 **[建立連結報表]**。  
  
2.  輸入新連結報表的名稱。 選擇性地輸入描述。  
  
3.  若要選取報表的其他資料夾，請按一下 **[變更位置]**。 按一下您要使用的資料夾，或者在 **[位置]** 方塊中輸入資料夾名稱。 [!INCLUDE[clickOK](../../includes/clickok-md.md)] 如果您未選取其他資料夾，則會在目前的資料夾 (儲存基準報表的位置) 中建立連結報表。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 連結報表隨即開啟。  
  
     連結報表的圖示與報表伺服器所管理的其他項目不同。 下列圖示表示連結報表：  
  
     ![連結報表圖示](../../reporting-services/report-server/media/hlp-16linked.gif "連結報表圖示")  
  
## <a name="see-also"></a>另請參閱  
 [開啟及關閉報表 &#40;報表管理員&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [新增連結報表頁面 &#40;報表管理員&#41;](https://msdn.microsoft.com/library/fefb46e8-6901-4d50-a3f8-7c49ad72e7b1)   
 [選擇項目位置頁面 &#40;報表管理員&#41;](https://msdn.microsoft.com/library/4a53a1a8-d1e1-47ef-b1fc-63352ece7d3c)   
 [一般屬性頁面，報表 &#40;報表管理員&#41;](https://msdn.microsoft.com/library/66c99d28-ab41-45f0-bf02-ed560293595d)   
 [Reporting Services 概念 &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
