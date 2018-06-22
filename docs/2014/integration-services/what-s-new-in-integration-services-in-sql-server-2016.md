---
title: 什麼&#39;s 新 (Integration Services) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
caps.latest.revision: 112
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c7d37fb3c1d2cd1dcafecc012fbe83e1864e50ed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023574"
---
# <a name="what39s-new-integration-services"></a>什麼&#39;s 新 (Integration Services)
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 維持與舊版相同。  
  
 如需其他資訊[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]產品和技術，請參閱[What's New in SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md)。  
  
 如需有關相關變更[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]商業智慧，請參閱[What's New in Analysis Services 和 Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md)。  
  
##  <a name="ValidateXML"></a> XML 工作中詳細的 XML 驗證輸出  
 驗證 XML 文件，啟用以取得詳細的錯誤輸出`ValidationDetails`XML 工作的屬性。 之前`ValidationDetails`屬性可用，XML 工作所執行的 XML 驗證只會傳回 true 或 false 結果，而不相關的錯誤或其位置資訊。 現在，當您將`ValidationDetails`為 true 時，輸出檔包含有關每個錯誤，包括行號及位置的詳細的資訊。 您可以使用此資訊來了解、尋找及修正 XML 文件中的錯誤。 如需詳細資訊，請參閱＜ [Validate XML with the XML Task](control-flow/xml-task.md)＞。  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 導入`ValidationDetails`屬性[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]Service Pack 2。 這項新的屬性目前尚未經過宣布或記載。 `ValidationDetails`屬性也會提供[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]和 SQL Server 2016 中。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 各版本所支援的功能](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  