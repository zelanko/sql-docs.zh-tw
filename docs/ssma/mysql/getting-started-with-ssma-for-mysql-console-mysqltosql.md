---
title: 開始使用 SSMA for MySQL 主控台 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- MySQL Console, launching console
- MySQL Console, output conventions
ms.assetid: 218d502c-059f-4d48-9aea-61e553d74303
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 07c1c226d33a213dd9bd071c59d9771a0e0ca736
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63183041"
---
# <a name="getting-started-with-ssma-for-mysql-console-mysqltosql"></a>開始使用 SSMA for MySQL 主控台 (MySQLToSQL)
本章節描述的程序啟動並開始使用 MySQL 主控台應用程式。 也列出，此處所使用的慣例典型的 SSMA 主控台輸出 視窗中。  
  
## <a name="launching-ssma-console"></a>啟動 SSMA 主控台  
您可以使用下列步驟來啟動 SSMA 主控台應用程式：  
  
1.  移至**開始**，指向**所有程式**。  
  
2.  按一下  **SQL Server Migration Assistant for MySQL 命令提示字元**捷徑。  
  
    它會顯示 [SSMA 主控台使用方式] 功能表和`(/? Help)`，以協助您開始使用主控台應用程式。  
  
## <a name="procedure-for-using-the-ssma-console"></a>使用 SSMA 主控台程序  
Windows 系統上成功啟動主控台後，您可以使用下列步驟，在其上運作：  
  
1.  設定 SSMA 主控台中的指令碼檔案。 如需有關此區段的詳細資訊，請參閱[建立指令碼檔案&#40;MySQLToSQL&#41; ](../../ssma/mysql/creating-script-files-mysqltosql.md) 。  
  
2.  [建立變數值檔案&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
3.  [建立伺服器連線檔案&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
4.  [執行 SSMA 主控台&#40;MySQLToSQL&#41; ](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)根據您的專案需求  
  
其他功能：  
  
1.  [保護密碼](managing-passwords-mysqltosql.md)並匯出 / 匯入到其他視窗機器  
  
2.  [產生報表](generating-reports-mysqltosql.md)以檢視詳細的 xml 輸出評估 /conversion 和資料移轉的報表。 詳細的錯誤報告也可能產生的重新整理] 和 [同步處理命令。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 主控台輸出慣例  
執行 SSMA 指令碼命令和選項，主控台程式會在主控台上對使用者顯示的結果和訊息 （資訊、 錯誤等），或如有需要，將重新導向至 xml 輸出檔。 每一種在輸出中的訊息被以獨特的色彩。 例如，在白色文字訊息表示指令碼檔案的命令;綠色的色彩中的一個表示提示使用者輸入，依此類推。  
  
![SSMAConsoleOutput_MySQL](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
下表中的主控台輸出的色彩解譯：  
  
|色彩|描述|  
|---------|---------------|  
|紅色|在執行期間的嚴重錯誤|  
|灰色|日期和時間戳記，訊息給使用者|  
|白皮書|指令碼檔案的命令、 訊息類型|  
|黃色|警告|  
|綠色|提示使用者輸入|  
|11：青色|開始]、 [完成] 和 [作業的結果。|  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for MySQL](installing-ssma-for-mysql-mysqltosql.md)  
  
