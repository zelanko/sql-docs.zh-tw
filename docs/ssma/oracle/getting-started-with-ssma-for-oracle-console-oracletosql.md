---
title: 開始使用 SSMA for Oracle 主控台 (OracleToSQL) |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Oracle Console, Console Output Conventions
- Oracle Console, Launching Console
ms.assetid: 667a5e4a-6848-4973-a72d-1287f64718ac
caps.latest.revision: 31
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: f80a1d1dde407c2269a29c4c18c0ad583dc39b93
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34777314"
---
# <a name="getting-started-with-ssma--for-oracle-console-oracletosql"></a>開始使用 SSMA for Oracle 主控台 (OracleToSQL)
本章節描述的程序啟動並開始使用 Oracle 的主控台應用程式。 亦會使用的慣例典型的 SSMA 主控台輸出視窗中。  
  
## <a name="launching-ssma-console"></a>啟動 SSMA 主控台  
若要啟動 SSMA 主控台應用程式中使用下列步驟：  
  
1.  移至**啟動**指向**所有程式**。  
  
2.  按一下**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉小幫手的 Oracle 命令提示字元**捷徑。  
  
    它會顯示 [SSMA 主控台使用方式] 功能表和`(/? Help)`，以協助您開始使用主控台應用程式。  
  
## <a name="procedure-for-using-the-ssma-console"></a>針對使用 SSMA 主控台的程序  
Windows 系統上已成功啟動主控台之後，您可以在 bob_ws 上工作使用下列步驟：  
  
1.  透過指令碼檔案中設定 SSMA 主控台。 如需有關本章節的詳細資訊，請參閱[建立指令碼檔&#40;OracleToSQL&#41; ](../../ssma/oracle/creating-script-files-oracletosql.md) 。  
  
2.  [建立變數值的檔案&#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
3.  [建立伺服器連接檔案&#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
4.  [執行 SSMA 主控台&#40;OracleToSQL&#41; ](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)根據您的專案需求  
  
其他功能：  
  
1.  [指定密碼](http://msdn.microsoft.com/en-us/8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c)及匯出 / 匯入其他視窗機器  
  
2.  [產生報告](http://msdn.microsoft.com/en-us/ccad6262-01e1-447a-bd2b-c105154c80ce)以檢視詳細的 xml 輸出評估 /conversion 和資料移轉的報表。 詳細的錯誤報表也可以產生重新整理] 和 [同步處理的命令。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 主控台輸出慣例  
時執行的 SSMA 指令碼命令和選項，主控台程式會在主控台上對使用者顯示的結果和訊息 （資訊、 錯誤等），或如果需要，重新導向至 xml 輸出檔。 在輸出訊息的每個型別被以獨特的色彩。 例如，白色文字訊息表示指令碼檔案的命令;綠色中的一個代表提示使用者輸入，依此類推。  
  
![SSMA 主控台 Output_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "SSMA 主控台 Output_Oracle")  
  
下表中的主控台輸出的色彩解譯：  
  
|Color|描述|  
|---------|---------------|  
|紅色|執行期間發生嚴重錯誤|  
|灰色|日期和時間戳記，訊息給使用者|  
|白色|編寫指令碼檔案的命令、 訊息類型|  
|黃色|警告|  
|綠色|提示使用者輸入|  
|11：青色|開始、 完成和作業的結果。|  
  
## <a name="see-also"></a>另請參閱  
[安裝的 SSMA for Oracle](http://msdn.microsoft.com/en-us/9211013a-ab24-4c52-9b26-87994b35e502)  
  
