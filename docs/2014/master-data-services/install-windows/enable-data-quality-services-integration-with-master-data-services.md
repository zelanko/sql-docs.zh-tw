---
title: 啟用 Data Quality Services 與 Master Data Services 的整合 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ab32938d-a80e-4106-80d4-94b2de3d67dc
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7248c23349ae8ab5c307a4b33c02bd2301c0b572
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034158"
---
# <a name="enable-data-quality-services-integration-with-master-data-services"></a>啟用 Data Quality Services 與 Master Data Services 的整合
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，比對功能是由 Data Quality Services (DQS) 提供。 此功能必須啟用才能使用。  
  
## <a name="prerequisites"></a>必要條件  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 應用程式和資料庫必須存在。  
  
-   Data Quality Services 功能和 Data Quality Client 必須安裝在裝載 MDS 資料庫的相同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。 如需詳細資訊，請參閱 [安裝 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)。  
  
### <a name="to-enable-data-quality-services-integration"></a>若要啟用 Data Quality Services 整合  
  
1.  開啟 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
2.  按一下左窗格中的 **[Web 組態]**。  
  
3.  在 [Web 組態] 頁面上，選取網站和 Web 應用程式。  
  
4.  在 [啟用 DQS 整合] 區段中，按一下 [啟用與 Data Quality Services 整合]。  
  
5.  在確認對話方塊中按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [資料品質比對中的 MDS 增益集的 Excel](../microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [適用於 Microsoft Excel 的 Master Data Services 增益集](../microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)   
 [安裝 Master Data Services](install-master-data-services.md)  
  
  