---
description: 開始使用 SSMA for MySQL 主控台 (MySQLToSQL)
title: 使用 SSMA for MySQL 主控台的消費者入門 (MySQLToSQL) |Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 9eba640bc529487772510e06a7c66210be3e43a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463437"
---
# <a name="getting-started-with-ssma-for-mysql-console-mysqltosql"></a>開始使用 SSMA for MySQL 主控台 (MySQLToSQL)
本節說明啟動和開始使用 MySQL 主控台應用程式的程式。 本文也列出一般 SSMA 主控台輸出視窗中所使用的慣例。  
  
## <a name="launching-ssma-console"></a>啟動 SSMA 主控台  
使用下列步驟來啟動 SSMA 主控台應用程式：  
  
1.  移至 [ **開始** ]，然後指向 [ **所有程式**]。  
  
2.  按一下 [ **適用于 MySQL 的 SQL Server 移轉小幫手命令提示** 字元] 快捷方式。  
  
    它會顯示 [SSMA 主控台使用方式] 功能表和 `(/? Help)` ，以協助您開始使用主控台應用程式。  
  
## <a name="procedure-for-using-the-ssma-console"></a>使用 SSMA 主控台的程式  
在 Windows 系統上成功啟動主控台之後，您可以使用下列步驟來處理它：  
  
1.  透過指令檔設定 SSMA 主控台。 如需本節的詳細資訊，請參閱 [建立指令檔 &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-script-files-mysqltosql.md) 。  
  
2.  [建立變數值檔案 &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
3.  [建立伺服器連接檔案 &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
4.  根據您的專案需求[，執行 SSMA 主控台 &#40;MySQLToSQL&#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)  
  
其他功能：  
  
1.  [保護密碼](managing-passwords-mysqltosql.md) 並將它匯出/匯入到其他視窗電腦  
  
2.  [產生報表](generating-reports-mysqltosql.md) ，以查看詳細的 xml 輸出報告以進行評定/conversion 和資料移轉。 也可以針對重新整理和同步處理命令產生詳細的錯誤報表。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 主控台輸出慣例  
執行 SSMA 指令碼命令和選項時，主控台程式會 (資訊、錯誤等等顯示結果和訊息，) 到主控台上的使用者或需要時，重新導向至 xml 輸出檔。 輸出中的每個訊息類型都是以唯一的色彩表示。 例如，白色的文字訊息表示腳本檔案命令;綠色的色彩表示提示輸入使用者輸入，依此類推。  
  
![SSMAConsoleOutput_MySQL](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
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
[安裝適用于 MySQL 的 SSMA](installing-ssma-for-mysql-mysqltosql.md)  
  
