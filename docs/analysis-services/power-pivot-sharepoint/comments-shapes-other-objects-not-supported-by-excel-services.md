---
title: "註解、 形狀、 Excel Services 不支援其他物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ade92e15-dfbf-496b-9378-a00bd83ba750
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bb73f60aea4a67a2e7fe7967dc9411762fe8e8f9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="comments-shapes-other-objects-not-supported-by-excel-services"></a>註解、 形狀，Excel Services 不支援其他物件
  當您從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 欄位清單將交叉分析篩選器加入 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿時，將會發生這個錯誤。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用對象|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Excel Web Access 無法轉譯形狀物件，該物件用來控制從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 欄位清單加入活頁簿之交叉分析篩選器的位置和格式。|  
|訊息文字|下列功能不受 Excel Services 的支援，而且可能不會顯示或是只顯示一部分：<br /><br /> 註解、形狀或其他物件<br /><br /> 某些功能 (例如外部資料查詢) 會顯示只能在 Microsoft Excel 中重新整理的快取資料。|  
  
## <a name="explanation"></a>說明  
 當您在瀏覽器中開啟 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿而且按一下此訊息的 [詳細資料] 按鈕時，Excel Web Access 會顯示這個錯誤：**不支援的功能。此活頁簿可能無法以預期中的方式顯示**。  
  
 發生這個錯誤是因為 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿包含交叉分析篩選器，此交叉分析篩選器的配置是由 Excel 中的隱藏形狀物件所控制。 形狀物件會控制交叉分析篩選器在水平和垂直位置的格式與定位。  
  
 Excel Services 無法轉譯形狀物件，但是因為此物件是隱藏的，所以它無法轉譯的事實並不會造成問題。  
  
## <a name="user-action"></a>使用者動作  
 可以忽略這個錯誤。 按一下 [確定]，關閉錯誤訊息，並繼續使用活頁簿和交叉分析篩選器，而不會發生任何問題。  
  
  

