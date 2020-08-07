---
title: 消費者入門使用適用于 Access 主控台的 SSMA (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e9ca0ef87aac60849d114d0e43dd349e063e8c83
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938508"
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>消費者入門使用適用于 Access 主控台的 SSMA (AccessToSQL) 
本節說明啟動和開始使用存取主控台應用程式的程式。 這裡也列出了一般 SSMA 主控台輸出視窗中所使用的慣例。  
  
## <a name="launching-ssma-console"></a>啟動 SSMA 主控台  
使用下列步驟來啟動 SSMA 主控台應用程式：  
  
1.  移至 [**開始**] 並指向 [**所有程式**]。  
  
2.  按一下 [**存取命令提示**字元] 快捷方式的 [SQL Server 移轉小幫手]。  
  
    它會顯示 SSMA 主控台的 [使用方式] 功能表 `(/? Help)` ，並協助您開始使用主控台應用程式。  
  
## <a name="procedure-for-using-the-ssma-console"></a>使用 SSMA 主控台的程式  
在 Windows 系統上成功啟動主控台之後，您可以使用下列步驟來處理它：  
  
1.  透過腳本檔案設定 SSMA 主控台。 如需本節的詳細資訊，請參閱[&#40;AccessToSQL&#41;建立腳本](../../ssma/access/creating-script-files-accesstosql.md)檔。  
  
2.  [建立變數值檔案 &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [&#40;AccessToSQL 建立伺服器連接檔案&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  根據您的專案需求[，執行 SSMA 主控台 &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
其他功能：  
  
1.  [指定密碼](managing-passwords-accesstosql.md)，並將它匯出/匯入到其他視窗機器  
  
2.  [產生報告](generating-reports-accesstosql.md)以查看詳細的 xml 輸出報告，以進行評估/conversion 和資料移轉。 也可以針對重新整理和同步處理命令產生詳細的錯誤報表。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 主控台輸出慣例  
執行 SSMA 指令碼命令和選項時，主控台程式會在主控台上顯示結果和訊息 (資訊、) 錯誤等等，或在必要時，將會重新導向至 xml 輸出檔。 輸出中的每個訊息類型都是以唯一的色彩表示。 例如，以白色顯示的文字訊息代表腳本檔案命令;綠色色彩中的一個代表使用者輸入的提示，依此類推。  
  
![SSMA 控制台輸出](../../ssma/access/media/ssmaconsoleoutput.jpg "SSMA 控制台輸出")  
  
下表中主控台輸出的色彩轉譯：  
  
|Color|描述|  
|---------|---------------|  
|紅色|執行期間發生嚴重錯誤|  
|灰色|日期和時間戳記，訊息給使用者|  
|白色|指令檔命令，訊息類型|  
|黃色|警告|  
|綠色|提示使用者輸入|  
|11：青色|作業的開始、結束和結果|  
  
## <a name="see-also"></a>另請參閱  
[安裝 SQL Server 移轉小幫手以進行存取](installing-sql-server-migration-assistant-for-access-accesstosql.md)  
  
