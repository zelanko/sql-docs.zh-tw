---
title: 指令碼工作範例 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], examples
- examples [Integration Services]
- SSIS Script task, examples
ms.assetid: b0dd77ee-ee11-4cd9-87aa-61dd67f2fe1c
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5fc17272161d3f93618ddd4e559bb630efdd50ae
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37322598"
---
# <a name="script-task-examples"></a>指令碼工作範例
  指令碼工作是多用途的工具，可用於封裝中以滿足 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所含的工作無法達成的幾乎任何需求。 本主題列出指令碼工作程式碼範例，以示範某些可用的功能。  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用這些指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
### <a name="example-topics"></a>範例主題  
 本章節包含程式碼範例，以示範各種可合併到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 指令碼工作中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 類別：  
  
 [以指令碼工作偵測空的一般檔案](../extending-packages-scripting-task-examples/detecting-an-empty-flat-file-with-the-script-task.md)  
 檢查一般檔案以判斷它是否包含資料列，並將結果儲存到變數中，以供在控制流程分支中使用。  
  
 [以指令碼工作收集 Foreach 迴圈的清單](../extending-packages-scripting-task-examples/gathering-a-list-for-the-foreach-loop-with-the-script-task.md)  
 蒐集符合使用者指定的準則之檔案清單，並填入變數以供稍後由 Foreach From Variable 列舉值使用。  
  
 [以指令碼工作查詢 Active Directory](../extending-packages-scripting-task-examples/querying-the-active-directory-with-the-script-task.md)  
 使用 System.DirectoryServices 命名空間中的類別，根據 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 變數值，從 Active Directory 擷取使用者資訊。  
  
 [以指令碼工作監視效能計數器](../extending-packages-scripting-task-examples/monitoring-performance-counters-with-the-script-task.md)  
 使用 System.Diagnostics 命名空間中的類別，建立可用以追蹤 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件執行進度的自訂效能計數器。  
  
 [以指令碼工作處理影像](../extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md)  
 透過使用 System.Drawing 命名空間中的類別，將影像壓縮成 JPEG 格式，並從其中建立縮圖影像。  
  
 [以指令碼工作尋找安裝的印表機](../extending-packages-scripting-task-examples/finding-installed-printers-with-the-script-task.md)  
 透過使用 System.Drawing.Printing 命名空間中的類別，尋找支援特定紙張大小的已安裝印表機。  
  
 [以指令碼工作傳送 HTML 郵件訊息](../extending-packages-scripting-task-examples/sending-an-html-mail-message-with-the-script-task.md)  
 以 HTML 格式，而不是純文字格式傳送郵件訊息。  
  
 [以指令碼工作處理 Excel 檔案](../extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
 列出 Excel 檔案中的工作表，並檢查特定工作表是否存在。  
  
 [以指令碼工作傳送至遠端私用訊息佇列](../extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md)  
 將訊息傳送至遠端私用訊息佇列。  
  
### <a name="other-examples"></a>其他範例  
 下列主題也包含與指令碼工作搭配使用的程式碼範例：  
  
 [在指令碼工作中使用變數](../extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 根據可能超過另一個變數中所指定之上限的封裝變數值，詢問使用者是否確定封裝應該繼續執行。  
  
 [在指令碼工作中連線至資料來源](../extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 從定義在封裝中的連接管理員，擷取連接或是連接資訊。  
  
 [在指令碼工作中引發事件](../extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 根據伺服器上的網際網路連接狀態，引發錯誤、警告或是參考用訊息。  
  
 [在指令碼工作中記錄](../extending-packages-scripting/task/logging-in-the-script-task.md)  
 將工作所處理的項目數目記錄到啟用的記錄提供者。  
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期  **<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
  
