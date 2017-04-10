---
title: "活頁簿中的資料連接路徑指向本機磁碟機上的檔案或者是無效的 URI。 下列連接無法重新整理：Power Pivot 資料 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: bd22e41a-0931-4d32-888a-633a3046fc5e
caps.latest.revision: 7
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 活頁簿中的資料連接路徑指向本機磁碟機上的檔案或者是無效的 URI。 下列連接無法重新整理：Power Pivot 資料
  如果是包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的 Excel 活頁簿，Excel Services 會在無法連接到內嵌資料來源時傳回這個錯誤。  
  
## 詳細資料  
  
|||  
|-|-|  
|適用對象|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Excel Services 設定為只允許來自信任資料連線庫中 .odc 檔案的資料連接。|  
|訊息文字|活頁簿中的資料連接路徑指向本機磁碟機上的檔案或者是無效的 URI。 下列連接無法重新整理︰ [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料|  
  
## 說明  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿包含內嵌資料連接。 若要透過交叉分析篩選器和篩選器來支援活頁簿互動，Excel Services 必須設定為可允許透過內嵌連接資訊來進行外部資料存取。 若要擷取伺服器陣列中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器上所載入的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料，需進行外部資料存取。  
  
## 使用者動作  
 變更組態設定來允許內嵌資料來源連線。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]**。  
  
2.  按一下 [Excel Services 應用程式]。  
  
3.  按一下 [信任的檔案位置]。  
  
4.  按一下 [http://] 或是您想要設定的位置。  
  
5.  在 [外部資料] 中，於 [允許外部資料] 內按一下 [信任的資料連線庫與內嵌連線]。  
  
6.  按一下 **[確定]**。  
  
 或者，您可以針對包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿的網站建立新的信任位置，然後只針對該網站修改組態設定。 如需詳細資訊，請參閱[在管理中心建立 Power Pivot 網站的信任位置](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
  