---
title: 選擇資料來源或驅動程式 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], selecting driver
- connecting to data source [ODBC], selecting data source
- data sources [ODBC], selecting
- ODBC drivers [ODBC], selecting
ms.assetid: 10aaf570-01ab-4478-8339-bdde2a5e3dd1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b10aafad95463f56ec0f5a029eac59a02cff003b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303369"
---
# <a name="choosing-a-data-source-or-driver"></a>選擇資料來源或驅動程式
應用程式使用的數據源或驅動程式有時在應用程式中是硬編碼的。 例如,MIS 部門編寫的將數據從一個數據源傳輸到另一個數據源的自定義應用程式將包含這些數據源的名稱-該應用程式根本不適用於任何其他資料來源。 另一個範例是垂直應用程式,例如用於訂單輸入的應用程式。 此類應用程式始終使用相同的數據源,該數據源具有應用程式已知的預定義架構。  
  
 其他應用程式在運行時選擇數據源或驅動程式。 通常,這些是執行臨時查詢的通用應用程式,例如使用ODBC導入資料的電子表格。 此類應用程式通常列出可用的數據源或驅動程式,並允許使用者選擇要使用的數據源或驅動程式。 通用應用程式是否經常列出數據源、驅動程式或兩者,取決於應用程式是使用基於 DBMS 還是基於檔的驅動程式。  
  
 基於 DBMS 的驅動程式通常需要一組複雜的連接資訊,例如網路位址、網路協定、資料庫名稱等。 數據源的目的是隱藏所有這些資訊。 因此,數據源範例可用於基於 DBMS 的驅動程式。 應用程式可以通過以下兩種方式之一向使用者顯示數據源清單。 它可以使用**DSN(** 資料來源名稱)關鍵字調用**SQLDriverConnect,** 並且沒有關聯的值;驅動程式管理員將顯示資料來源名稱的清單。 如果應用程式希望控制列表的外觀,它將調用**SQLDataSources**來檢索可用數據來源的清單並建構其自己的對話方塊。 此功能由驅動程式管理器實現,可以在載入任何驅動程式之前調用。 然後,應用程式調用連接函數並傳遞所選數據源的名稱。  
  
 如果未指定數據源,則使用系統資訊指示的預設數據源。 (關於詳細資訊,請參考[預設子鍵](../../../odbc/reference/install/default-subkey.md)。如果使用找不到的*伺服器Name*參數、空指標或"DEFAULT"呼叫**SQLConnect,** 則驅動程式管理員將連接到預設資料來源。 如果調用**SQLDriverConnect**或**SQLBrowseConnect**中使用的連接字串包含設置為"DEFAULT"的**DSN**關鍵字,或者找不到指定的數據源,則還會使用預設資料源。 此外,如果調用**SQLDriverConnect**中使用的連接字串不包含**DSN**關鍵字,則使用預設數據源。  
  
 使用基於檔的驅動程式,可以使用檔範例。 對於存儲在本地電腦上的數據,用戶經常知道他們的數據位於特定檔中,如 Employ.dbf。 此類使用者可以更輕鬆地選擇他們知道的檔,而不是選擇未知的數據源。 為了實現這一點,應用程式首先呼叫**SQLDrivers**。 此功能由驅動程式管理器實現,可以在載入任何驅動程式之前調用。 **SQLDrivers**傳回可用驅動程式的清單;它還返回**檔案使用方式**和**檔Extn**關鍵字的值。 **FileUsage**關鍵字解釋基於檔的驅動程式是像 Xbase 一樣將檔案視為表,還是將檔視為資料庫,Microsoft®訪問也是如此。 **FileExtns**關鍵字列出了驅動程式識別的檔名副檔名,例如 Xbase 驅動程式的 .dbf。 使用此資訊,應用程式將建構一個對話框,用戶通過該對話方塊選擇檔。 從選取的檔案的副檔名,應用程式然後透過 DRIVER 關鍵字呼叫**SQLDriverConnect**連接到**驅動程式**。  
  
 沒有什麼可以阻止應用程式使用具有基於檔的驅動程式的數據來源,或者使用**DRIVER**關鍵字呼叫**SQLDriverConnect**以連接到基於 DBMS 的驅動程式。 以下是基於 DBMS 的**驅動程式**的 DRIVER 關鍵字的幾個常見用途:  
  
-   **不創建數據源。** 例如,自定義應用程式可能使用特定的驅動程式和資料庫。 如果驅動程式名稱和連接到資料庫所需的所有資訊在應用程式中是硬編碼的,則使用者不必在其電腦上創建數據源即可運行應用程式。 他們必須做的是安裝應用程式和驅動程式。  
  
     此方法的缺點是,如果連接資訊發生更改,則必須重新編譯和重新分發應用程式。 如果在應用程式中硬編碼數據來源名稱,而不是完整的連接資訊,則每個用戶必須僅更改數據源中的資訊。  
  
-   **一次訪問特定的 DBMS。** 例如,透過調用ODBC函數檢索資料的電子表格可能包含用於標識特定驅動程式的**DRIVER**關鍵字。 由於驅動程式名稱對於任何具有該驅動程式的使用者都有意義,因此可以在這些用戶之間傳遞電子錶格。 如果電子表格包含數據來源名稱,則每個使用者必須創建相同的數據來源才能使用電子表格。  
  
-   **流覽特定驅動程式可存取的所有資料庫的系統。** 有關詳細資訊,請參閱本節後面的[SQLBrowseConnect 連接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。
