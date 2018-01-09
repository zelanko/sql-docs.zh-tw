---
title: "無效的資料連接路徑 |Microsoft 文件"
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
ms.assetid: bd22e41a-0931-4d32-888a-633a3046fc5e
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b74fcdb45f2f7fb85423da9faa629e3565b10209
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="the-data-connection-path-is-invalid"></a>資料連接路徑無效
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]包含的 Excel 活頁簿[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]資料，Excel Services 會傳回這個錯誤，如果它無法連接到內嵌的資料來源。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用對象|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Excel Services 設定為只允許來自信任資料連線庫中 .odc 檔案的資料連接。|  
|訊息文字|活頁簿中的資料連接路徑指向本機磁碟機上的檔案或者是無效的 URI。 下列連接無法重新整理︰ [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿包含內嵌資料連線。 若要透過交叉分析篩選器和篩選器來支援活頁簿互動，Excel Services 必須設定為可允許透過內嵌連接資訊來進行外部資料存取。 若要擷取伺服器陣列中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器上所載入的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料，需進行外部資料存取。  
  
## <a name="user-action"></a>使用者動作  
 變更組態設定來允許內嵌資料來源連線。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]**。  
  
2.  按一下 [Excel Services 應用程式]。  
  
3.  按一下 [信任的檔案位置]。  
  
4.  按一下 [http://] 或是您想要設定的位置。  
  
5.  在 [外部資料] 中，於 [允許外部資料] 內按一下 [信任的資料連線庫與內嵌連線]。  
  
6.  按一下 [確定] 。  
  
 或者，您可以針對包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿的網站建立新的信任位置，然後只針對該網站修改組態設定。 如需詳細資訊，請參閱[在管理中心建立 Power Pivot 網站的信任位置](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
  
