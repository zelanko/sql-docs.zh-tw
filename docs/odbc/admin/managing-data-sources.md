---
title: 管理資料來源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9dc741321894ae69a9ffb59738576a01d47628f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901662"
---
# <a name="managing-data-sources"></a>管理資料來源
您已安裝 ODBC 驅動程式從驅動程式的安裝程式之後，您可以為它定義一或多個資料來源。 資料來源名稱 (DSN) 應該提供唯一的資料描述例如，*薪資*或是*Accounts Payable*。 所有目前安裝的驅動程式所定義的使用者和系統資料來源所述**使用者 DSN**或是**系統 DSN**索引標籤的**ODBC 資料來源管理員** 對話方塊。 檔案資料來源，在指定的目錄中所述**檔案 DSN**索引標籤，顯示的目錄進入**查看**方塊中**檔案 DSN**  索引標籤。  
  
> [!NOTE]  
>  若要管理的資料來源，連接到 32 位元驅動程式在 64 位元平台，使用 c:\windows\sysWOW64\odbcad32.exe。 若要管理的資料來源，連接到 64 位元驅動程式，請使用 c:\windows\system32\odbcad32.exe。 在 [**系統管理工具**64 位元 Windows 8 作業系統上有 32 位元和 64 位元圖示**ODBC 資料來源管理員**] 對話方塊。  
  
 如果您要設定或移除 DSN 連線至 32 位元驅動程式，比方說，使用 64 位元 odbcad32.exe**驅動程式執行 Microsoft Access (\*.mdb)** ，您會收到下列錯誤訊息：  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 若要解決這個錯誤，請使用 32 位元 odbcad32.exe 要設定或移除資料來源名稱。  
  
 資料來源會將特定的 ODBC 驅動程式與您想要透過該驅動程式存取的資料產生關聯。 例如，您可能會建立要使用 ODBC dBASE 驅動程式來存取您的硬碟或網路磁碟機上的特定目錄中找到的一或多個 dBASE 檔案的資料來源。 使用 ODBC 資料來源管理員，您可以新增、 修改及刪除資料來源下, 表中所述。  
  
|Action|描述|  
|------------|-----------------|  
|新增資料來源|可以新增多個資料來源，每個驅動程式關聯至您想要使用該驅動程式存取部分的資料。 指定每個資料來源的名稱可唯一識別該資料來源。 比方說，如果您建立一組 dBASE 檔案包含客戶資訊的資料來源時，您可能會指定名稱的資料來源 「 客戶 」。 應用程式通常會顯示使用者可從中選擇的資料來源名稱。<br /><br /> 加入檔案資料來源會稍有不同於新增使用者或系統資料來源。 如需詳細資訊，請參閱說明檔的 ODBC 資料來源管理員。|  
|修改資料來源|根據您的需求，您可能會發現需要重新設定資料來源。 您可以將選項重設，即可**設定**任何驅動程式安裝程式 對話方塊中。|  
|刪除資料來源|按一下 **移除**選取資料來源之後。|  
  
 如需檔案資料來源的詳細資訊，請參閱[連線使用的檔案資料來源](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)或[SQLDriverConnect 函數](../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)
