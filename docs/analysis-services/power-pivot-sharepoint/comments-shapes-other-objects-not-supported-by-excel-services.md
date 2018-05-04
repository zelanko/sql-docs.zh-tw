---
title: 註解、 形狀、 Excel Services 不支援其他物件 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6bd1c2224c9c75859f2314599799066d27152d79
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="comments-shapes-other-objects-not-supported-by-excel-services"></a>註解、 形狀，Excel Services 不支援其他物件
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  當您從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 欄位清單將交叉分析篩選器加入 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿時，將會發生這個錯誤。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用對象|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|제품 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Excel Web Access 無法轉譯形狀物件，該物件用來控制從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 欄位清單加入活頁簿之交叉分析篩選器的位置和格式。|  
|메시지 텍스트|下列功能不受 Excel Services 的支援，而且可能不會顯示或是只顯示一部分：<br /><br /> 註解、形狀或其他物件<br /><br /> 某些功能 (例如外部資料查詢) 會顯示只能在 Microsoft Excel 中重新整理的快取資料。|  
  
## <a name="explanation"></a>說明  
 當您在瀏覽器中開啟 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿而且按一下此訊息的 [詳細資料] 按鈕時，Excel Web Access 會顯示這個錯誤：**不支援的功能。此活頁簿可能無法以預期中的方式顯示**。  
  
 發生這個錯誤是因為 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿包含交叉分析篩選器，此交叉分析篩選器的配置是由 Excel 中的隱藏形狀物件所控制。 形狀物件會控制交叉分析篩選器在水平和垂直位置的格式與定位。  
  
 Excel Services 無法轉譯形狀物件，但是因為此物件是隱藏的，所以它無法轉譯的事實並不會造成問題。  
  
## <a name="user-action"></a>使用者動作  
 可以忽略這個錯誤。 按一下 [確定]，關閉錯誤訊息，並繼續使用活頁簿和交叉分析篩選器，而不會發生任何問題。  
  
  
