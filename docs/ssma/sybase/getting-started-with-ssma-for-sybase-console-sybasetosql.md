---
title: 開始使用 SSMA for Sybase 主控台 (SybaseToSQL) |Microsoft Docs
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: bad08c06028a64a0423135b15641ebf6fa4e895e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029116"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>開始使用 SSMA for Sybase 主控台 (SybaseToSQL)
本章節描述的程序啟動並開始使用 SSMA for Sybase 主控台應用程式。 也列出本文件所使用的慣例典型的 SSMA 主控台輸出 視窗中。  
  
## <a name="launching-the-ssma-console"></a>啟動 SSMA 主控台  
您可以使用下列步驟來啟動 SSMA 主控台應用程式：  
  
1.  請移至 開始、，然後指向 所有程式。  
  
2.  按一下  **SQL Server Migration Assistant for Sybase 命令提示字元**捷徑。  
  
    它會顯示 [SSMA 主控台使用方式] 功能表和`(/? Help)`，以協助您開始使用主控台應用程式。  
  
## <a name="using-the-ssma-console"></a>使用 SSMA 主控台  
Windows 系統上成功啟動主控台後，您可以使用下列步驟，在其上運作：  
  
1.  設定 SSMA 主控台中的指令碼檔案。 如需有關此區段的詳細資訊，請參閱[建立指令碼檔案&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md)。  
  
2.  [建立變數值檔案&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [建立伺服器連線檔案&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [執行 SSMA 主控台&#40;SybaseToSQL&#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)根據您的專案需求。 
  
其他功能：  
  
1.  [指定密碼](managing-passwords-sybasetosql.md)和匯出/匯入它到視窗中的其他電腦。  
  
2.  [產生報表](generating-reports-sybasetosql.md)以檢視詳細的 xml 輸出的評量/轉換和資料移轉報告。 您也可以產生詳細的錯誤報表重新整理] 和 [同步處理命令。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 主控台輸出慣例  
執行 SSMA 指令碼命令和選項，主控台程式會向使用者在主控台上顯示的結果和訊息 （資訊、 錯誤等） 或如有必要，將重新導向至 xml 輸出檔。 每一種在輸出中的訊息被以獨特的色彩。 例如，在白色文字訊息表示指令碼檔案的命令;綠色的色彩中的一個表示提示使用者輸入，依此類推。  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
下表中，會出現色彩-解譯的主控台輸出：  
  
|色彩|描述|  
|---------|---------------|  
|紅色|在執行期間的嚴重錯誤|  
|灰色|日期和時間戳記，訊息給使用者|  
|白皮書|指令碼檔案的命令、 訊息類型|  
|黃色|警告|  
|綠色|提示使用者輸入|  
|11：青色|開始時間、 完成時間和作業的結果。|  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
