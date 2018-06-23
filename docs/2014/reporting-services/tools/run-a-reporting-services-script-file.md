---
title: 執行 Reporting Services 指令碼檔案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scripts [Reporting Services], running
ms.assetid: 0de4995c-85ec-4d4c-aaef-fbd30edfb20f
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 06a2631c737654ad1fc0041f5a919a57db4acc43
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145776"
---
# <a name="run-a-reporting-services-script-file"></a>執行 Reporting Services 指令碼檔案
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 指令碼檔案是使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 指令碼環境 (RS.exe)，從命令提示字元執行。 RS.exe 包含多個命令提示字元引數供您使用。 如需命令提示字元選項的詳細資訊，請參閱 [RS.exe 公用程式 &#40;SSRS&#41;](rs-exe-utility-ssrs.md)。 如需其他指令碼範例，請參閱 [SQL Server Reporting Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="sample-command-lines"></a>範例命令列  
  
-   在指令碼環境中執行 Script.rss 以指定目標報表伺服器。 預設會套用 Windows 驗證：  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver  
    ```  
  
-   在指令碼環境中執行 Script.rss 以指定驗證 Web 服務呼叫的使用者名稱和密碼：  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -u myusername -p mypassword  
    ```  
  
-   在指令碼環境中執行 Script.rss 以指定 30 秒的伺服器逾時：  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -l 30  
    ```  
  
-   在指令碼環境中執行 Script.rss 以指定稱為 *report*的全域指令碼 (Global Script) 變數。  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -v report="Company Sales"  
    ```  
  
-   在指令碼環境中執行 Script.rss 以指定指令碼檔案中的 Web 服務作業以批次方式執行。  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -b  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [技術參考 &#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  