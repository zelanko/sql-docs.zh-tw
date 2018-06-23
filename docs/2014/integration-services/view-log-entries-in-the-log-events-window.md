---
title: 在 [記錄事件] 視窗中檢視記錄項目 |Microsoft 文件
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
- logs [Integration Services], viewing
- Integration Services packages, logs
- packages [Integration Services], logs
ms.assetid: c02123c3-67fc-4370-ad14-91ed259f1873
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: fb92bd7899e1d35d8ca816356c9618709964bb13
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144752"
---
# <a name="view-log-entries-in-the-log-events-window"></a>檢視記錄事件視窗中的記錄項目
  此程序描述如何執行封裝並檢視封裝寫入的記錄項目。 您可以即時檢視記錄項目， 也可以複製及儲存寫入 [記錄事件] 視窗中的記錄項目，以執行進一步的分析。  
  
 您不需要將記錄項目寫入記錄檔，以便將項目寫入 [記錄事件] 視窗中。  
  
### <a name="to-view-log-entries"></a>檢視記錄項目  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [SSIS] 功能表上，按一下 [記錄事件]。 您可以將 View.LogEvents 命令對應到您在 [選項] 對話方塊的 [鍵盤] 頁面中所選擇的組合鍵，以選擇性地顯示 [記錄事件] 視窗。  
  
3.  在 **[偵錯]** 功能表上，按一下 **[開始偵錯]**。  
  
     當執行階段遇到為了記錄而啟用的事件與自訂訊息時，每個事件或訊息的記錄項目都會寫入 [記錄事件] 視窗。  
  
4.  在 **[偵錯]** 功能表上，按一下 **[停止偵錯]**。  
  
     記錄項目將繼續保留在 [記錄事件] 視窗中，直到您重新執行封裝、執行不同的封裝或關閉 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 為止。  
  
5.  檢視 [記錄事件] 視窗中的記錄項目。  
  
6.  (選擇性) 按一下要複製的記錄項目，按一下滑鼠右鍵，然後按一下 [複製]。  
  
7.  (選擇性) 按兩下記錄項目，然後在 [記錄項目] 對話方塊中檢視單一記錄項目的詳細資料。  
  
8.  在 [記錄項目] 對話方塊中，按一下上下箭頭以顯示上一個或下一個記錄項目，然後按一下複製圖示來複製記錄項目。  
  
9. 開啟文字編輯器、貼上，然後將記錄項目儲存為文字檔。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 記錄](performance/integration-services-ssis-logging.md)  
  
  