---
title: 步驟 5：測試更新的封裝 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: 683e52e5-1c7e-49ab-9ffe-6a450a1c5776
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 07da75fc6f7f703d5767b393ea662904dd6a1c36
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-5---testing-the-updated-packages"></a>課程 1-5 - 測試更新的封裝
在進入下一課之前，請先測試封裝，因為在下一課中，您將會建立部署配套，以便在目的地電腦上用來安裝教學課程封裝。 在這項工作中，您會執行 DataTransfer.dtsx 和 LoadXMLData 封裝，這兩個封裝都已加入至「部署教學課程」專案中，並且以組態進行擴充。  
  
當封裝執行時，封裝中的每一個可執行檔在順利完成後都會變成綠色。 當所有可執行檔都變成綠色時，就表示該封裝已順利完成。 您也可以在 [進度] 索引標籤上檢視套件的執行進度。  
  
如果封裝未能順利執行，則必須加以修正，才能進入下一課。  
  
### <a name="to-run-the-datatransfer-package"></a>若要執行 DataTransfer 封裝  
  
1.  在 [方案總管] 中，按一下 DataTransfer.dtsx。  
  
2.  在 **[偵錯]** 功能表上，按一下 **[開始偵錯]**。  
  
3.  在封裝完成執行之後，在 **[偵錯]** 功能表上，按一下 **[停止偵錯]**。  
  
### <a name="to-run-the-loadxmldata-package"></a>若要執行 LoadXMLData 封裝  
  
1.  在 [方案總管] 中，按一下 LoadXMLData.dtsx。  
  
2.  在 **[偵錯]** 功能表上，按一下 **[開始偵錯]**。  
  
3.  在封裝完成執行之後，在 **[偵錯]** 功能表上，按一下 **[停止偵錯]**。  
  
## <a name="next-lesson"></a>下一課  
[第 2 課：在 SSIS 中建立部署配套](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
  
  
  
