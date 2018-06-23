---
title: 儲存活頁簿的信任位置不允許外部資料連接。 下列連接無法重新整理： PowerPivot 資料 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dc0cedfd-a7d0-40ef-bdd6-ea508130640a
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 449ac77f0eaff4a5d3550711b18ec57751460918
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023210"
---
# <a name="the-trusted-location-where-the-workbook-is-stored-does-not-allow-external-data-connections-the-following-connections-failed-to-refresh-powerpivot-data"></a>儲存活頁簿的信任位置不允許外部資料連接。 下列連接無法重新整理：PowerPivot 資料
  如果是包含 PowerPivot 資料的 Excel 活頁簿，Excel Services 會在無法連接到內嵌資料來源時傳回這個錯誤。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用對象|PowerPivot for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Excel Services 設定為拒絕外部資料存取。|  
|訊息文字|儲存活頁簿的信任位置不允許外部資料連接。 下列連接無法重新整理：PowerPivot 資料|  
  
## <a name="explanation"></a>說明  
 PowerPivot 活頁簿包含內嵌資料連接。 若要透過交叉分析篩選器和篩選器來支援活頁簿互動，Excel Services 必須設定為可允許透過內嵌連接資訊來進行外部資料存取。 擷取伺服陣列中 PowerPivot 伺服器上所載入的 PowerPivot 資料時，需要外部資料存取。  
  
## <a name="user-action"></a>使用者動作  
 變更組態設定來允許內嵌資料來源。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]**。  
  
2.  按一下 [Excel Services 應用程式]。  
  
3.  按一下 [信任的檔案位置]。  
  
4.  按一下 [http://] 或是您想要設定的位置。  
  
5.  在 [外部資料] 中，於 [允許外部資料] 內按一下 [信任的資料連線庫與內嵌連線]。  
  
6.  按一下 [確定] 。  
  
 或者，您可以針對包含 PowerPivot 活頁簿的網站建立新的信任位置，然後只針對該網站修改組態設定。 如需相關資訊，請參閱 [Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
  