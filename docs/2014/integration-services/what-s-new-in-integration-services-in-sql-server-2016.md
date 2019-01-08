---
title: 什麼&#39;s 新 (Integration Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 804e528aed70a6612f35391bd4ad96ebfd03df3a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52792010"
---
# <a name="what39s-new-integration-services"></a>什麼&#39;s 新 (Integration Services)
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 維持與舊版相同。  
  
 如需其他資訊[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]產品和技術，請參閱[What's New in SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md)。  
  
 如需有關變更的相關[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]商業智慧，請參閱 < [What's New in Analysis Services 和 Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md)。  
  
##  <a name="ValidateXML"></a> XML 工作中詳細的 XML 驗證輸出  
 驗證 XML 文件，並啟用 XML 工作的 `ValidationDetails` 屬性以取得詳細的錯誤輸出。 在提供 `ValidationDetails` 屬性前，XML 工作所執行的 XML 驗證只會傳回結果為 True 或 False，而不會有錯誤的相關資訊及其位置。 現在，當您將 `ValidationDetails` 設定為 True 時，輸出檔案即涵蓋每項錯誤的詳細資訊，包括行號及位置。 您可以使用此資訊來了解、尋找及修正 XML 文件中的錯誤。 如需詳細資訊，請參閱＜ [Validate XML with the XML Task](control-flow/xml-task.md)＞。  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 2 中引進了 `ValidationDetails` 屬性。 這項新的屬性目前尚未經過宣布或記載。 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 及 SQL Server 2016 也提供 `ValidationDetails` 屬性。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 各版本所支援的功能](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
