---
title: "受信任位置不允許外部資料連接 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: dc0cedfd-a7d0-40ef-bdd6-ea508130640a
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 84dcf4dd95bc3848e6e8f0e66478f8fc99e2b3f2
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="trusted-location-does-not-allow-external-data-connections"></a>受信任的位置不允許外部資料連接
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
如果是包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的 Excel 活頁簿，Excel Services 會在無法連接到內嵌資料來源時傳回這個錯誤。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用對象|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|제품 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Excel Services 設定為拒絕外部資料存取。|  
|訊息文字|儲存活頁簿的信任位置不允許外部資料連接。 下列連接無法重新整理︰ [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿包含內嵌資料連線。 若要透過交叉分析篩選器和篩選器來支援活頁簿互動，Excel Services 必須設定為可允許透過內嵌連接資訊來進行外部資料存取。 若要擷取伺服器陣列中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器上所載入的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料，需進行外部資料存取。  
  
## <a name="user-action"></a>사용자 동작  
 變更組態設定來允許內嵌資料來源。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]**。  
  
2.  按一下 [Excel Services 應用程式]。  
  
3.  按一下 [信任的檔案位置]。  
  
4.  按一下 [http://] 或是您想要設定的位置。  
  
5.  在 [外部資料] 中，於 [允許外部資料] 內按一下 [信任的資料連線庫與內嵌連線]。  
  
6.  按一下 **[確定]**。  
  
 或者，您可以針對包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿的網站建立新的信任位置，然後只針對該網站修改組態設定。 如需詳細資訊，請參閱[在管理中心建立 Power Pivot 網站的信任位置](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
  
