---
title: 選擇資料來源或驅動程式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c238b89f6fefbb158c50531d28d2c234c64f64bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63125464"
---
# <a name="choosing-a-data-source-or-driver"></a>選擇資料來源或驅動程式
資料來源或應用程式所使用的驅動程式有時會硬式編碼應用程式中。 比方說，撰寫由 MIS 部門傳送到另一個資料來源資料會包含名稱的自訂應用程式的這些資料來源的應用程式根本不能運作與任何其他資料來源。 另一個範例是垂直的應用程式，例如一個用於訂單項目。 這類應用程式一律使用相同的資料來源都有已知的應用程式的預先定義結構描述。  
  
 其他應用程式會在執行階段選取資料來源或驅動程式。 這些通常是進行臨機操作查詢，例如試算表，以使用 ODBC 將資料匯入的一般應用程式。 這類應用程式通常會列出可用的資料來源或驅動程式，並讓使用者選擇他們想要使用的項目。 是否泛型應用程式會列出資料來源、 驅動程式，或兩者通常取決於應用程式是否使用以 DBMS 為基礎，或檔案為基礎的驅動程式。  
  
 以 DBMS 為基礎的驅動程式通常需要一組複雜的連接資訊，例如網路位址、 網路通訊協定、 資料庫名稱等等。 資料來源的目的是要隱藏所有的這項資訊。 因此，資料來源模式本身還需要以 DBMS 為基礎的驅動程式搭配使用。 應用程式可以在兩種方式之一中的使用者顯示資料來源的清單。 它可以呼叫**SQLDriverConnect**具有**DSN** （資料來源名稱） 關鍵字和任何相關聯的值; 驅動程式管理員會顯示資料來源名稱的清單。 如果應用程式想要控制清單的外觀，則會呼叫**SQLDataSources**擷取一份可用資料來源並建構自己的對話方塊。 此函式實作由驅動程式管理員，而且可以在任何驅動程式載入之前呼叫。 應用程式然後呼叫連線函式，並將它傳遞所選的資料來源的名稱。  
  
 如果未指定資料來源，則會使用預設的系統資訊所指出的資料來源。 (如需詳細資訊，請參閱 <<c0> [ 預設子機碼](../../../odbc/reference/install/default-subkey.md)。)如果**SQLConnect**透過呼叫*ServerName*找不到、 為 null 指標，或為"DEFAULT"的引數，驅動程式管理員會連接到預設資料來源。 如果連接字串，也會使用資料來源的預設值會在呼叫**SQLDriverConnect**或是**SQLBrowseConnect**包含**DSN**關鍵字設定為 「 預設"或如果找不到指定的資料來源。 此外，如果連接字串，使用資料來源，則預設會在呼叫**SQLDriverConnect** neobsahuje **DSN**關鍵字。  
  
 以檔案為基礎的驅動程式，就可以使用檔案架構。 對於資料儲存在本機電腦上，使用者經常會知道其資料是在特定的檔案，例如 Employee.dbf。 而不是選取的未知的資料來源，是選取的檔案才會知道這類使用者更容易。 若要這樣做，應用程式會先呼叫**SQLDrivers**。 此函式實作由驅動程式管理員，而且可以在任何驅動程式載入之前呼叫。 **SQLDrivers**會傳回一份可用的驅動程式; 它也會傳回值**FileUsage**並**FileExtns**關鍵字。 **FileUsage**關鍵字說明是否檔案為基礎的驅動程式將視為資料表，做為檔案沒有 Xbase，或做為資料庫，為 Microsoft® Access。 **FileExtns**關鍵字列出驅動程式會辨識，例如 Xbase 驅動程式的.dbf 檔案名稱副檔名。 使用這項資訊，應用程式會建構一個對話方塊，讓使用者選擇檔案。 根據所選檔案的副檔名，然後在應用程式連接到驅動程式藉由呼叫**SQLDriverConnect**具有**驅動程式**關鍵字。  
  
 沒有要阻止某個應用程式的檔案為基礎的驅動程式搭配使用的資料來源，或呼叫**SQLDriverConnect**具有**驅動程式**關鍵字來連線到以 DBMS 為基礎的驅動程式。 以下是幾個常見的用法**驅動程式**關鍵字以 DBMS 為基礎的驅動程式：  
  
-   **無法建立資料來源。** 例如，自訂應用程式可能會使用特定驅動程式和資料庫。 如果驅動程式名稱和連接到資料庫所需的所有資訊都是硬式編碼應用程式中，使用者不必在其執行應用程式的電腦上建立資料來源。 他們必須做的只是安裝在應用程式和驅動程式。  
  
     這個方法的缺點是應用程式必須重新編譯，而且如果連接資訊變更，轉散發。 如果資料來源名稱是硬式編碼應用程式，而不是完整的連接資訊中，每位使用者必須變更資料來源中的資訊。  
  
-   **存取特定的 DBMS 一次。** 例如，可能會包含藉由呼叫 ODBC 函數會擷取資料的試算表**驅動程式**關鍵字來識別特定的驅動程式。 驅動程式名稱是以任何具有該驅動程式的使用者有意義，因為無法傳遞試算表，這些使用者。 如果試算表包含資料來源名稱，每位使用者必須建立要使用試算表相同的資料來源。  
  
-   **瀏覽至特定的驅動程式可存取的所有資料庫的系統。** 如需詳細資訊，請參閱 <<c0> [ 使用 sqldriverconnect 進行連接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)稍後這一節。
