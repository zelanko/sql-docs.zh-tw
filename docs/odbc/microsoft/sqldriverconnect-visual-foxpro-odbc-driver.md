---
title: "SQLDriverConnect （Visual FoxPro ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 363a727cd209f7ed3a5994f353f1e21922fe00ca
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect （Visual FoxPro ODBC 驅動程式）
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 完整  
  
 ODBC 應用程式開發介面相容性： 層級 1  
  
 連接到現有的資料來源，可為[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)或目錄的[釋放資料表](../../odbc/microsoft/visual-foxpro-terminology.md)。 UID 和 PWD ODBC 屬性關鍵字會被忽略。 下表列出支援的其他屬性的關鍵字。  
  
|ODBC 屬性關鍵字|屬性值|  
|----------------------------|---------------------|  
|DSN||  
|UID|Visual FoxPro ODBC 驅動程式所忽略，但不會產生錯誤。|  
|PWD|Visual FoxPro ODBC 驅動程式所忽略，但不會產生錯誤。|  
|驅動程式|名稱和位置的 Visual FoxPro ODBC 驅動程式。實作由驅動程式管理員。|  
  
|Visual FoxPro ODBC 驅動程式屬性的關鍵字|屬性值|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Yes"或者"No"|  
|自動分頁|「 機器 」 或其他定序順序。 如需支援的定序順序的清單，請參閱[設定 COLLATE](../../odbc/microsoft/set-collate-command.md)。|  
|Description||  
|排除|"Yes"或者"No"|  
|SourceDB|完整的路徑到目錄，包含零或多個[釋放資料表](../../odbc/microsoft/visual-foxpro-terminology.md)，或是的絕對路徑和檔案名稱[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)。|  
|SourceType|「 雙位元組字元"或者"DBF"|  
|Version||  
  
 如果未指定資料來源名稱，驅動程式管理員 會提示使用者輸入資訊 (視設定而定*fDriverCompletion*引數) 然後繼續進行。 如果需要詳細資訊，Visual FoxPro ODBC 驅動程式會顯示提示的對話方塊。  
  
 如需詳細資訊，請參閱[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)中*ODBC 程式設計人員參考*。
