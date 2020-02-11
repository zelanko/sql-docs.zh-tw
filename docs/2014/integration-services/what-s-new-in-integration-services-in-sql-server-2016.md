---
title: 新的&#39;（Integration Services） |Microsoft Docs
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5562b7424e4a104204becaed10378ffc999c4e98
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68891109"
---
# <a name="what39s-new-integration-services"></a>新的&#39;（Integration Services）
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]與舊版不相同。  
  
 如需其他[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]產品和技術的相關資訊，請參閱[SQL Server 2014 中的新功能](../sql-server/what-s-new-in-sql-server-2016.md)。  
  
 如需[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]商業智慧相關變更的詳細資訊，請參閱[Analysis Services 和商業智慧的新功能](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)。  
  
##  <a name="ValidateXML"></a>XML 工作中的豐富 XML 驗證輸出  
 驗證 XML 文件，並啟用 XML 工作的 `ValidationDetails` 屬性以取得詳細的錯誤輸出。 在提供 `ValidationDetails` 屬性前，XML 工作所執行的 XML 驗證只會傳回結果為 True 或 False，而不會有錯誤的相關資訊及其位置。 現在，當您將 `ValidationDetails` 設定為 True 時，輸出檔案即涵蓋每項錯誤的詳細資訊，包括行號及位置。 您可以使用此資訊來了解、尋找及修正 XML 文件中的錯誤。 如需詳細資訊，請參閱＜ [Validate XML with the XML Task](control-flow/xml-task.md)＞。  
  
 
  [!INCLUDE[ssIS](../includes/ssis-md.md)] 在 `ValidationDetails` Service Pack 2 中引進了 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 屬性。 這項新的屬性目前尚未經過宣布或記載。 
  `ValidationDetails` 及 SQL Server 2016 也提供 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 屬性。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 各版本所支援的功能](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
