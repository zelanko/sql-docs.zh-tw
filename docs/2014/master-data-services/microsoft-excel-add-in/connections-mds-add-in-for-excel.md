---
title: 連接 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 2f2b2f9d-7744-460e-83cd-56d34ea70ff0
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a7d336e777f4f6bf00310cbadfed75987ba45252
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65478935"
---
# <a name="connections-mds-add-in-for-excel"></a>連接 (適用於 Excel 的 MDS 增益集)
  若要將資料下載至 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，您必須先建立連接。 連接可讓 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 服務知道要連接的目標 MDS 資料庫。  
  
 連接字串通常是 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式的 URL，例如 http://contoso/mds。  
  
 每次您啟動 Excel 時，都必須連接到 MDS 儲存機制。 唯一的例外狀況是使用中試算表已經包含 MDS 管理的資料。 在此情況中，每次您重新整理或發行工作表中的資料時，系統就會自動建立連接。  
  
 您可以建立多個連接。 最近存取的連接會被視為預設值。  
  
 多位使用者可以同時進行連接。 不過，當多位使用者嘗試發行相同的資料時，可能會引發衝突。 如需詳細資訊，請參閱[發行 Data &#40;適用于 Excel 的 MDS 增益集&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)。  
  
## <a name="connect-automatically-and-load-frequently-used-data"></a>自動連接並載入經常使用的資料  
 如果您想要永遠連接到相同的伺服器並且載入相同的資料集，可以建立包含連接和篩選資訊的捷徑查詢檔案。 如需查詢檔案的詳細資訊，請參閱 [捷徑查詢檔案 &#40;適用於 Excel 的 MDS 增益集&#41;](shortcut-query-files-mds-add-in-for-excel.md)。  
  
## <a name="data-quality-services"></a>Data Quality Services  
 
  [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 具有 Data Quality Services 功能，可協助您在發行資料至 MDS 儲存機制之前比對資料。 當您建立連接時，如果 DQS 資料庫與 MDS 資料庫安裝在相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上，您就能夠在功能區上檢視 DQS 按鈕。 如果 DQS_Main 資料庫不存在執行個體上，系統就不會顯示這些按鈕，而且資料品質功能將無法使用。  
  
## <a name="troubleshooting-connections"></a>疑難排解連接  
 當您連接到 MDS 時，如果您遇到任何問題[https://social.technet.microsoft.com/wiki/contents/articles/4520.aspx](https://social.technet.microsoft.com/wiki/contents/articles/4520.aspx) ，請參閱以取得疑難排解秘訣。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|建立 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫的連接。|[連接到適用于 Excel 的 mds 增益集 &#40;的 MDS 儲存機制&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|將 MDS 資料載入 Excel 中。|[將資料從 MDS 載入 Excel 中](export-data-to-excel-from-master-data-services.md)|  
|在將 MDS 資料載入 Excel 之前篩選資料。|[載入 &#40;適用于 Excel 的 MDS 增益集之前先篩選資料&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [載入適用于 Excel 的 MDS 增益集&#41;的資料 &#40;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [&#40;適用于 Excel 的 MDS 增益集的快捷方式查詢檔案&#41;](shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [適用於 Microsoft Excel 的 Master Data Services 增益集](master-data-services-add-in-for-microsoft-excel.md)  
  
  
