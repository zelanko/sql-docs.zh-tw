---
title: "選擇資料來源或驅動程式 |Microsoft 文件"
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
- connecting to driver [ODBC], selecting driver
- connecting to data source [ODBC], selecting data source
- data sources [ODBC], selecting
- ODBC drivers [ODBC], selecting
ms.assetid: 10aaf570-01ab-4478-8339-bdde2a5e3dd1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f7263f7814e4ab286d1fd678604b3f84a45108f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="choosing-a-data-source-or-driver"></a>選擇資料來源或驅動程式
資料來源或應用程式所使用的驅動程式是有時候硬式編碼應用程式中。 比方說，自訂撰寫的應用程式所要傳送 MIS 部門會包含這些資料來源的名稱，到另一個資料來源資料，應用程式只會無法搭配任何其他資料來源。 另一個範例是垂直應用程式，例如其中一個用於訂單項目。 這類應用程式一律使用相同的資料來源，具有預先定義的結構描述的應用程式知道。  
  
 其他應用程式會在執行階段選取資料來源或驅動程式。 這些通常是進行臨機操作查詢，例如使用 ODBC 將資料匯入試算表的泛型應用程式。 這類應用程式通常會列出可用的資料來源或驅動程式，並讓使用者選擇他們想要使用的項目。 是否泛型應用程式列出資料來源、 驅動程式，或兩者通常取決於應用程式是否使用 DBMS 或檔案為基礎的驅動程式。  
  
 DBMS 架構驅動程式通常需要一組複雜的連接資訊，例如網路位址、 網路通訊協定、 資料庫名稱等等。 資料來源的目的是要隱藏所有的這項資訊。 因此，資料來源開發架構本身 DBMS 架構驅動程式搭配使用。 應用程式可以顯示資料來源的清單中有兩種使用者。 它可以呼叫**SQLDriverConnect**與**DSN** （資料來源名稱） 關鍵字和相關聯的值; 驅動程式管理員會顯示資料來源名稱的清單。 如果應用程式想控制清單的外觀，則會呼叫**SQLDataSources**擷取一份可用資料來源，建構自己的對話方塊。 此函數會實作由驅動程式管理員，並可以在任何驅動程式在載入之前呼叫。 應用程式接著會呼叫連線函式，並將它傳遞至所選的資料來源的名稱。  
  
 如果未指定資料來源，則會使用預設的系統資訊所指出的資料來源。 (如需詳細資訊，請參閱[預設子機碼](../../../odbc/reference/install/default-subkey.md)。)如果**SQLConnect**呼叫使用*ServerName*找不到、 為 null 指標，或為"DEFAULT"的引數，驅動程式管理員會連接到預設資料來源。 如果連接字串，也會使用資料來源的預設值用於呼叫**SQLDriverConnect**或**SQLBrowseConnect**包含**DSN**關鍵字設定為 「 預設值"或如果找不到指定的資料來源。 此外，如果連接字串，使用資料來源會使用的預設的呼叫中**SQLDriverConnect**不包含**DSN**關鍵字。  
  
 透過以檔案為基礎的驅動程式，就可以使用檔案範例。 資料儲存在本機電腦上，使用者經常會知道其資料是在特定的檔案中，例如 Employee.dbf。 而不是選取未知的資料來源，是選取的檔案才會知道這類使用者更容易。 若要實作此應用程式的第一個呼叫**SQLDrivers**。 此函數會實作由驅動程式管理員，並可以在任何驅動程式在載入之前呼叫。 **SQLDrivers**會傳回一份可用的驅動程式; 它也會傳回值**FileUsage**和**FileExtns**關鍵字。 **FileUsage**關鍵字說明是否以檔案為基礎的驅動程式將檔案都視為資料表，做為沒有 Xbase，還是做為資料庫，做為 Microsoft® Access。 **FileExtns**關鍵字列出辨識驅動程式，例如 Xbase 驅動程式的.dbf 檔案名稱的副檔名。 使用這項資訊，應用程式建構，使用者選擇檔案 對話方塊。 根據所選的檔案的副檔名，然後在應用程式會連接到驅動程式呼叫**SQLDriverConnect**與**驅動程式**關鍵字。  
  
 沒有要停止從資料來源使用以檔案為基礎的驅動程式，或呼叫應用程式項目**SQLDriverConnect**與**驅動程式**關鍵字來連線到 DBMS 架構驅動程式。 以下是幾個常見的用法**驅動程式**DBMS 架構驅動程式的關鍵字：  
  
-   **無法建立資料來源。** 例如，自訂的應用程式可能會使用特定驅動程式和資料庫。 如果驅動程式名稱和連接到資料庫所需的所有資訊都是硬式編碼應用程式中，使用者不必執行應用程式的電腦上建立資料來源。 管理員必須執行所有已安裝的應用程式和驅動程式。  
  
     這個方法的缺點是必須重新編譯應用程式，並重新發佈的連接資訊變更時。 如果資料來源名稱是硬式編碼而不是完整的連線資訊的應用程式中，每位使用者必須變更資料來源中的資訊。  
  
-   **存取特定 DBMS 一次。** 例如，可能包含擷取資料，藉由呼叫 ODBC 函數的試算表**驅動程式**關鍵字來識別特定的驅動程式。 驅動程式名稱會有該驅動程式之任何使用者有意義，因為這些使用者之間傳遞試算表。 如果試算表包含資料來源名稱，每位使用者必須建立使用試算表相同的資料來源。  
  
-   **瀏覽到特定的驅動程式可存取的所有資料庫的系統。** 如需詳細資訊，請參閱[連接 SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)稍後在本章節中。

