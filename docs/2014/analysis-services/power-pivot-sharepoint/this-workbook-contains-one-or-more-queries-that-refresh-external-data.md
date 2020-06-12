---
title: 此活頁簿包含可重新整理外部資料的一個或多個查詢。 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: aa65c992-eb41-4032-9e11-a9ba871b6a3c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6e13b648b35cb0a6b6d9272ec9a2b9d560c3c7f4
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547740"
---
# <a name="this-workbook-contains-one-or-more-queries-that-refresh-external-data"></a>此活頁簿包含可重新整理外部資料的一個或多個查詢。
  對於包含 PowerPivot 資料的 Excel 活頁簿，Excel Services 會在偵測到連接資訊時顯示這個警告，然後提示您啟用或停用此活頁簿的查詢。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|PowerPivot for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Excel Services 設定為資料重新整理時警告。|  
|訊息文字|此活頁簿包含可重新整理外部資料的一個或多個查詢。 惡意使用者可以設計一個查詢來存取機密資訊，並將其散發給其他使用者或執行其他有害的動作。<br /><br /> 如果您信任此活頁簿的來源，按一下 [是]，啟用此活頁簿中對外部資料的查詢。 如果您不確定，按一下 [否]，變更就不會套用到您的活頁簿中。<br /><br /> 您要啟用此活頁簿中對外部資料的查詢嗎？|  
  
## <a name="explanation"></a>說明  
 PowerPivot 活頁簿包含內嵌的資料連接字串，Excel 會使用這些連接字串與載入和計算資料的外部 PowerPivot 伺服器進行通訊。 如果啟用資料重新整理時警告，Excel Services 會偵測此連接字串，並據此警告使用者。  
  
 若要篩選與配量活頁簿中的 PowerPivot 資料，必須啟用查詢。 請務必僅針對您信任的 PowerPivot 活頁簿啟用查詢。  
  
## <a name="user-action"></a>使用者動作  
 按一下 [是]**** 以啟用查詢。  
  
 您也可以變更組態設定，不再於重新整理時警告。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 [**管理服務應用程式**]。  
  
2.  按一下 [Excel Services 應用程式]****。  
  
3.  按一下 [信任的檔案位置]****。  
  
4.  按一下 [http://]**** 或是您想要設定的位置。  
  
5.  在 [外部資料] 中，清除 [Warn on data refresh (資料重新整理時警告)]**** 的核取方塊。  
  
6.  按一下 [確定]。  
  
 或者，您可以針對包含 PowerPivot 活頁簿的網站建立新的信任位置，然後只針對該網站修改組態設定。 如需相關資訊，請參閱 [Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
  
