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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901662"
---
# <a name="managing-data-sources"></a>管理資料來源
從驅動程式的安裝程式安裝 ODBC 驅動程式之後，您可以為它定義一或多個資料來源。 資料來源名稱（DSN）應提供資料的唯一描述;例如，*薪資*或*應付的帳戶*。 針對所有目前安裝的驅動程式所定義的使用者和系統資料來源，都會列在 [ **ODBC 資料來源管理員**] 對話方塊的 [**使用者 dsn** ] 或 [**系統 DSN** ] 索引標籤中。 指定目錄中的檔案資料來源會列在 [檔案**DSN** ] 索引標籤中;[檔案**DSN** ] 索引標籤的 [**查詢**] 方塊中會輸入要顯示的目錄。  
  
> [!NOTE]  
>  若要管理在64位平臺下連接到32位驅動程式的資料來源，請使用 c:\windows\sysWOW64\odbcad32.exe。 若要管理連接到64位驅動程式的資料來源，請使用 c:\windows\system32\odbcad32.exe。 在64位 Windows 8 作業系統的 [系統**管理工具**] 中，[32 位] 和 [64 位**ODBC 資料來源管理員**] 對話方塊都有圖示。  
  
 如果您使用 64-bit odbcad32.exe 來設定或移除連接到32位驅動程式的 DSN，例如， **driver Do Microsoft Access\*（.mdb）**，您將會收到下列錯誤訊息：  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 若要解決此錯誤，請使用 32-bit odbcad32.exe 來設定或移除 DSN。  
  
 資料來源會將特定 ODBC 驅動程式與您要透過該驅動程式存取的資料產生關聯。 例如，您可以建立資料來源來使用 ODBC dBASE 驅動程式，以存取在硬碟或網路磁碟機機上特定目錄中找到的一或多個 dBASE 檔案。 使用 [ODBC 資料來源管理員]，您可以加入、修改和刪除資料來源，如下表所述。  
  
|動作|描述|  
|------------|-----------------|  
|新增資料來源|您可以新增多個資料來源，每個都將驅動程式與您想要使用該驅動程式存取的某些資料產生關聯。 為每個資料來源指定可唯一識別該資料來源的名稱。 例如，如果您針對包含客戶資訊的一組 dBASE 檔案建立資料來源，您可以將資料來源命名為「Customers」。 應用程式通常會顯示資料來源名稱，供使用者選擇。<br /><br /> 新增檔案資料來源與加入使用者或系統資料來源有些微不同。 如需詳細資訊，請參閱 ODBC 資料來源管理員說明檔。|  
|修改資料來源|視您的需求而定，您可能會發現需要重新設定資料來源。 您可以按一下 [在任何驅動程式設定] 對話方塊中的 **[設定]** 來重設選項。|  
|刪除資料來源|選取資料來源之後，請按一下 [**移除**]。|  
  
 如需有關檔案資料來源的詳細資訊，請參閱[使用檔案資料來源連接](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)或[SQLDriverConnect 函數](../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)
