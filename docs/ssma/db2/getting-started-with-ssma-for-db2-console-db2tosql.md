---
description: '消費者入門與 DB2 主控台的 SSMA (DB2ToSQL) '
title: 消費者入門與 DB2 主控台的 SSMA (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f245c017-023e-4880-8721-8908d339525e
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 57cf454c5d13bf4a40325024e51bd19c4d56c446
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985097"
---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>消費者入門與 DB2 主控台的 SSMA (DB2ToSQL) 
本節說明啟動和開始使用 DB2 主控台應用程式的程式。 本文也列出一般 SSMA 主控台輸出視窗中所使用的慣例。  
  
## <a name="launching-ssma-console"></a>啟動 SSMA 主控台  
使用下列步驟來啟動 SSMA 主控台應用程式：  
  
1.  移至 [ **開始** ]，然後指向 [ **所有程式**]。  
  
2.  按一下** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MIGRATION ASSISTANT [DB2 命令提示**字元] 快捷方式。  
  
    它會顯示 [SSMA 主控台使用方式] 功能表和 `(/? Help)` ，以協助您開始使用主控台應用程式。  
  
## <a name="procedure-for-using-the-ssma-console"></a>使用 SSMA 主控台的程式  
在 Windows 系統上成功啟動主控台之後，您可以使用下列步驟來處理它：  
  
1.  透過指令檔設定 SSMA 主控台。 如需本節的詳細資訊，請參閱 [建立指令檔 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-script-files-db2tosql.md) 。  
  
2.  [建立變數值檔案 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [建立伺服器連接檔案 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  根據您的專案需求[，執行 SSMA 主控台 &#40;DB2ToSQL&#41;](../../ssma/db2/executing-the-ssma-console-db2tosql.md)  
  
其他功能：  
  
1.  [管理密碼](./managing-passwords-db2tosql.md) 以及將密碼匯出/匯入到其他視窗電腦  
  
2.  [產生報表](./generating-reports-db2tosql.md) ，以查看詳細的 xml 輸出報告以進行評定/conversion 和資料移轉。 也可以針對重新整理和同步處理命令產生詳細的錯誤報表。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 主控台輸出慣例  
執行 SSMA 指令碼命令和選項時，主控台程式會 (資訊、錯誤等等顯示結果和訊息，) 到主控台上的使用者或需要時，重新導向至 xml 輸出檔。 輸出中的每個訊息類型都是以唯一的色彩表示。 例如，白色的文字訊息表示腳本檔案命令;綠色的色彩表示提示輸入使用者輸入，依此類推。  
  
![SSMA Console Output_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "SSMA Console Output_Oracle")  
  
下表中的主控台輸出色彩解讀：  
  
|Color|描述|  
|---------|---------------|  
|紅色|執行期間發生嚴重錯誤|  
|灰色|日期和時間戳記，訊息給使用者|  
|白色|指令檔命令，訊息類型|  
|黃色|警告|  
|綠色|提示輸入使用者-輸入|  
|11：青色|作業的開始、完成和結果|  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for DB2](./installing-ssma-for-db2-db2tosql.md)  
