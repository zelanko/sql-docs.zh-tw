---
title: Word 裝置資訊設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7c6a084e7d2093d2f0bfc7d55ef7f16be5b83e1f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126874"
---
# <a name="word-device-information-settings"></a>Word 裝置資訊設定
  下表列出以 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 格式轉譯的裝置資訊設定。  
  
|設定|值|  
|-------------|-----------|  
|`AutoFit`|`False`. 都會將 AutoFit 設定為`false`在任何 Word 資料表上設定。<br /><br /> `True`. 在每個 Word 資料表上都會將 AutoFit 設定為 `true`。<br /><br /> `Never`. 在任何 Word 資料表上未設定 AutoFit 值，而且會將行為轉換 Word 預設值。<br /><br /> `Default`. 在每個邏輯頁上，AutoFit 是設定在比實體繪製區域 (排除邊界的實體頁面寬度) 更狹窄的資料表上。|  
|`ExpandToggles`|指出可以切換的所有項目是否應該以其完全展開的狀態來轉譯。 預設值是 `false`。|  
|`FixedPageWidth`|指定寫入 DOC 檔案的「頁面寬度」是否將配合「報表主體」中最大頁面的寬度來增加。 預設值是 `false`。|  
|**OmitHyperlinks**|指定在設定 Hyperlink 動作的位置上，是否在所有的項目上省略該動作。 預設值是 `false`|  
|`OmitDrillthroughs`|指定在設定 Drillthrough 動作的位置上，是否在所有的項目上省略該動作。 預設值是 `false`|  
  
## <a name="see-also"></a>另請參閱  
 [將裝置資訊設定傳遞至轉譯延伸模組](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
