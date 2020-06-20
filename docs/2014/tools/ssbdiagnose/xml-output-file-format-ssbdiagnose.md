---
title: XML 輸出檔案格式（ssbdiagnose） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose]
- ssbdiagnose
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 56758f15a3bd2a71221c936a80f7455d9e1c1cd9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85057614"
---
# <a name="xml-output-file-format-ssbdiagnose"></a>XML 輸出檔格式 (ssbdiagnose)
  當您執行 **ssbdiagnose** 公用程式搭配 **-XML** 參數時，此公用程式就會將其輸出傳遞成 XML 檔。 其 XML 輸出檔會列出標頭資訊以及它在分析之 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 組態或交談中找到的錯誤。 您可以撰寫應用程式來分析或報告該檔案中所列的錯誤。 或者，您可以在一般 XML 編輯器 (例如 XML Notepad) 中檢視此 XML 檔。  
  
 **ssbdiangose** 輸出檔包含具有兩種子類型的 DiagnosticInformation 根元素：  
  
-   具有標頭資訊的 Banner 元素。  
  
-   **ssbdiagnose**所報告之每個問題的 Issue 元素。  
  
## <a name="diagnosticinformation-root-element"></a>DiagnosticInformation 根元素  
  
-   [DiagnosticInformation 元素 &#40;ssbdiagnose&#41;](diagnosticinformation-element-ssbdiagnose.md)  
  
## <a name="banner-element"></a>Banner 元素  
  
-   [Banner 元素 &#40;ssbdiagnose&#41;](banner-element-ssbdiagnose.md)  
  
## <a name="issue-element"></a>Issue 元素  
  
-   [Issue 元素 &#40;ssbdiagnose&#41;](issue-element-ssbdiagnose.md)  
  
## <a name="see-also"></a>另請參閱  
 [ssbdiagnose 公用程式 &#40;Service Broker&#41;](ssbdiagnose-utility-service-broker.md)  
  
  
