---
description: '使用 SSMA for Sybase 主控台消費者入門 (SybaseToSQL) '
title: 使用 SSMA for Sybase 主控台消費者入門 (SybaseToSQL) |Microsoft Docs
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
ms.openlocfilehash: e59cb5565ca518dc927f29e684401bf8fc6d5822
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418314"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>使用 SSMA for Sybase 主控台消費者入門 (SybaseToSQL) 
本章節說明啟動和開始使用 SSMA for Sybase 主控台應用程式的程式。 本文也列出一般 SSMA 主控台輸出視窗中所使用的慣例。  
  
## <a name="launching-the-ssma-console"></a>啟動 SSMA 主控台  
使用下列步驟來啟動 SSMA 主控台應用程式：  
  
1.  移至 [開始]，然後指向 [所有程式]。  
  
2.  按一下 [ **Sybase 命令提示** 字元] 快捷方式的 SQL Server 移轉小幫手。  
  
    它會顯示 [SSMA 主控台使用方式] 功能表和 `(/? Help)` ，以協助您開始使用主控台應用程式。  
  
## <a name="using-the-ssma-console"></a>使用 SSMA 主控台  
在 Windows 系統上成功啟動主控台之後，您可以使用下列步驟來處理它：  
  
1.  透過指令檔設定 SSMA 主控台。 如需本節的詳細資訊，請參閱 [建立指令檔 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md)。  
  
2.  [建立變數值檔案 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [建立伺服器連接檔案 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  根據您的專案需求[，執行 SSMA 主控台 &#40;SybaseToSQL&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) 。 
  
其他功能：  
  
1.  [指定密碼](managing-passwords-sybasetosql.md) ，然後將其匯出/匯入到其他視窗電腦。  
  
2.  [產生報表](generating-reports-sybasetosql.md) ，以查看用於評估/轉換和資料移轉的詳細 xml 輸出報告。 您也可以產生重新整理和同步處理命令的詳細錯誤報表。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 主控台輸出慣例  
執行 SSMA 指令碼命令和選項時，主控台程式會在主控台上顯示 (資訊、錯誤等等 ) 的結果和訊息，或是在必要時將其重新導向至 xml 輸出檔。 輸出中的每個訊息類型都是以唯一的色彩表示。 例如，白色的文字訊息表示腳本檔案命令;綠色的色彩表示提示輸入使用者輸入，依此類推。  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
下表顯示主控台輸出的色彩解讀：  
  
|Color|描述|  
|---------|---------------|  
|紅色|執行期間發生嚴重錯誤|  
|灰色|日期和時間戳記，訊息給使用者|  
|白色|指令檔命令，訊息類型|  
|黃色|警告|  
|綠色|提示輸入使用者-輸入|  
|11：青色|作業的開始、完成和結果|  
  
## <a name="see-also"></a>另請參閱  
[安裝適用于 SAP ASE 的 SSMA &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
