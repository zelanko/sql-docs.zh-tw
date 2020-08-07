---
title: 消費者入門與 Sybase 主控台的 SSMA (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a577a2b187112dd0b80cedf50d42d13112208970
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87931551"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>消費者入門與 Sybase 主控台的 SSMA (SybaseToSQL) 
本節說明啟動和開始使用 SSMA for Sybase 主控台應用程式的程式。 這裡也列出一般 SSMA 主控台輸出視窗中使用的慣例。  
  
## <a name="launching-the-ssma-console"></a>啟動 SSMA 主控台  
使用下列步驟來啟動 SSMA 主控台應用程式：  
  
1.  移至 [開始]，然後指向 [所有程式]。  
  
2.  按一下 [ **Sybase 命令提示**字元] 快捷方式的 [SQL Server 移轉小幫手]。  
  
    它會顯示 SSMA 主控台的 [使用方式] 功能表 `(/? Help)` ，並協助您開始使用主控台應用程式。  
  
## <a name="using-the-ssma-console"></a>使用 SSMA 主控台  
在 Windows 系統上成功啟動主控台之後，您可以使用下列步驟來處理它：  
  
1.  透過腳本檔案設定 SSMA 主控台。 如需本節的詳細資訊，請參閱[&#40;SybaseToSQL&#41;建立腳本](../../ssma/sybase/creating-script-files-sybasetosql.md)檔。  
  
2.  [建立變數值檔案 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [&#40;SybaseToSQL 建立伺服器連接檔案&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  根據您的專案需求[，執行 SSMA 主控台 &#40;SybaseToSQL&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) 。 
  
其他功能：  
  
1.  [指定密碼](managing-passwords-sybasetosql.md)，並將它匯出/匯入到其他視窗電腦。  
  
2.  [產生報告](generating-reports-sybasetosql.md)以查看詳細的 xml 輸出報告，以進行評量/轉換和資料移轉。 您也可以針對 refresh 和同步處理命令產生詳細的錯誤報表。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 主控台輸出慣例  
在執行 SSMA 指令碼命令和選項時，主控台程式會在主控台上顯示結果和訊息 (資訊、) 錯誤等，或在必要時，將會重新導向至 xml 輸出檔。 輸出中的每個訊息類型都是以唯一的色彩表示。 例如，以白色顯示的文字訊息代表腳本檔案命令;綠色色彩中的一個代表使用者輸入的提示，依此類推。  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
主控台輸出的色彩解讀會出現在下表中：  
  
|Color|描述|  
|---------|---------------|  
|紅色|執行期間發生嚴重錯誤|  
|灰色|日期和時間戳記，訊息給使用者|  
|白色|指令檔命令，訊息類型|  
|黃色|警告|  
|綠色|提示使用者輸入|  
|11：青色|作業的開始、結束和結果|  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
