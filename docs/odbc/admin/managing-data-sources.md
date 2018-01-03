---
title: "管理資料來源 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ea157fd72ab1cc2b37ba32e198bde5ff47eff0fb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="managing-data-sources"></a>管理資料來源
您已安裝 ODBC 驅動程式從驅動程式的安裝程式之後，您可以為它定義一個或多個資料來源。 資料來源名稱 (DSN) 應該提供資料; 的唯一描述例如，*薪資*或*Accounts Payable*。 所有目前已安裝的驅動程式所定義使用者和系統資料來源會列在**使用者 DSN**或**系統 DSN**索引標籤的**ODBC 資料來源管理員** 對話方塊。 檔案資料來源，在指定的目錄中所述**檔案 DSN**索引標籤，以輸入要顯示的目錄是**查看**方塊中**檔案 DSN**  索引標籤。  
  
> [!NOTE]  
>  若要管理連線至 32 位元驅動程式在 64 位元平台的資料來源，使用 c:\windows\sysWOW64\odbcad32.exe。 若要管理的資料來源，連接到 64 位元驅動程式，請使用 c:\windows\system32\odbcad32.exe。 在**系統管理工具**64 位元 Windows 8 作業系統上有 32 位元和 64 位元的圖示**ODBC 資料來源管理員** 對話方塊。  
  
 如果您要設定或移除的 DSN 連接 32 位元驅動程式，例如，使用 64 位元 odbcad32.exe**驅動程式執行 Microsoft Access (\*.mdb)**，您會收到下列錯誤訊息：  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 若要解決這個錯誤，請使用 32 位元 odbcad32.exe 要設定或移除資料來源名稱。  
  
 資料來源會將特定的 ODBC 驅動程式與您想要透過該驅動程式存取的資料產生關聯。 例如，您可能會建立資料來源來存取您的硬碟或網路磁碟機上的特定目錄中找到的一或多個 dBASE 檔案使用 ODBC dBASE 驅動程式。 使用 ODBC 資料來源管理員，您可以新增、 修改和刪除資料來源下, 表中所述。  
  
|動作|描述|  
|------------|-----------------|  
|新增資料來源|它是可以加入多個資料來源，每個將驅動程式與您想要使用該驅動程式存取某些資料產生關聯。 提供每個資料來源的唯一識別該資料來源名稱。 例如，如果您建立一組 dBASE 檔案包含客戶資訊的資料來源，您可能會將資料來源 「 客戶 」。 應用程式通常會顯示使用者從選擇的資料來源名稱。<br /><br /> 加入檔案資料來源會稍有不同新增使用者或系統資料來源。 如需詳細資訊，請參閱說明檔的 ODBC 資料來源管理員。|  
|修改資料來源|根據您的需求，您可能會覺得必須重新設定資料來源。 您可以按一下 [重設選項**設定**任何驅動程式安裝程式] 對話方塊中。|  
|刪除資料來源|按一下**移除**選取資料來源之後。|  
  
 如需檔案資料來源的詳細資訊，請參閱[連接使用的檔案資料來源](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)或[SQLDriverConnect 函數](../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>請參閱  
 [ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)
