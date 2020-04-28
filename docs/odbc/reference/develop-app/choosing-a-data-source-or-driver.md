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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b10aafad95463f56ec0f5a029eac59a02cff003b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303369"
---
# <a name="choosing-a-data-source-or-driver"></a>選擇資料來源或驅動程式
應用程式所使用的資料來源或驅動程式有時會在應用程式中進行硬式編碼。 例如，由錯誤部門撰寫的自訂應用程式，會將資料從某個資料來源傳送至另一個，而不會包含這些資料來源的名稱-應用程式只會與任何其他資料來源搭配使用。 另一個範例是垂直應用程式，例如用來輸入訂單的一個。 這類應用程式一律會使用相同的資料來源，其具有應用程式已知的預先定義架構。  
  
 其他應用程式會在執行時間選取資料來源或驅動程式。 通常，這些是執行臨機操作查詢的一般應用程式，例如使用 ODBC 匯入資料的試算表。 這類應用程式通常會列出可用的資料來源或驅動程式，並讓使用者選擇他們想要使用的資源。 一般應用程式是否會列出資料來源、驅動程式，或兩者都經常取決於應用程式是使用 DBMS 型或以檔案為基礎的驅動程式。  
  
 以 DBMS 為基礎的驅動程式通常需要一組複雜的連接資訊，例如網路位址、網路通訊協定、資料庫名稱等等。 資料來源的目的是要隱藏所有這項資訊。 因此，資料來源架構本身會與 DBMS 型驅動程式搭配使用。 應用程式可以使用兩種方式的其中一種，將資料來源清單顯示給使用者。 它可以使用**DSN** （資料來源名稱）關鍵字和沒有相關聯的值來呼叫**SQLDriverConnect** 。[驅動程式管理員] 會顯示資料來源名稱的清單。 如果應用程式想要控制清單的外觀，它會呼叫**SQLDataSources**來抓取可用的資料來源清單，並建立自己的對話方塊。 此函式是由驅動程式管理員所執行，而且可以在載入任何驅動程式之前呼叫。 然後，應用程式會呼叫連接函式，並將所選資料來源的名稱傳遞給它。  
  
 如果沒有指定資料來源，則會使用系統資訊所指出的預設資料來源。 （如需詳細資訊，請參閱[預設](../../../odbc/reference/install/default-subkey.md)子機碼）。如果**SQLConnect**是使用找不到的*ServerName*引數所呼叫，則為 null 指標，或為 "Default"，驅動程式管理員會連接到預設的資料來源。 如果呼叫**SQLDriverConnect**或**SQLBrowseConnect**時所使用的連接字串包含設定為 "default" 的**DSN**關鍵字，或如果找不到指定的資料來源，也會使用預設的資料來源。 此外，如果在**SQLDriverConnect**的呼叫中使用的連接字串未包含**DSN**關鍵字，則會使用預設的資料來源。  
  
 透過以檔案為基礎的驅動程式，您可以使用檔案架構。 對於儲存在本機電腦上的資料，使用者經常知道其資料位於特定檔案中，例如 Employee .dbf。 不選取未知的資料來源，這類使用者可以更輕鬆地選取他們知道的檔案。 為了實現此，應用程式會先呼叫**SQLDrivers**。 此函式是由驅動程式管理員所執行，而且可以在載入任何驅動程式之前呼叫。 **SQLDrivers**會傳回可用驅動程式的清單;它也會傳回**FileUsage**和**FileExtns**關鍵字的值。 **FileUsage**關鍵字會說明以檔案為基礎的驅動程式是否將檔案視為資料表、Xbase 或資料庫，如同 Microsoft®存取。 **FileExtns**關鍵字會列出驅動程式可識別的副檔名，例如 Xbase 驅動程式的 .dbf。 應用程式會使用此資訊，來建立使用者選擇檔案的對話方塊。 根據所選檔案的副檔名，應用程式會使用**driver**關鍵字來呼叫**SQLDriverConnect** ，以連接到驅動程式。  
  
 不需要使用具有以檔案為基礎之驅動程式的資料來源來停止應用程式，或以**驅動**程式關鍵字呼叫**SQLDriverConnect**來連接到以 DBMS 為基礎的驅動程式。 以下是以 DBMS 為基礎的驅動程式之**DRIVER**關鍵字的幾個常見用法：  
  
-   **不建立資料來源。** 例如，自訂應用程式可能會使用特定的驅動程式和資料庫。 如果在應用程式中，連接到資料庫所需的驅動程式名稱和所有資訊都是硬式編碼，則使用者不需要在其電腦上建立資料來源來執行應用程式。 他們必須安裝應用程式和驅動程式。  
  
     這個方法的缺點是，如果連接資訊變更，就必須重新編譯和轉散發應用程式。 如果資料來源名稱在應用程式中是硬式編碼，而不是完整的連接資訊，則每個使用者都必須只變更資料來源中的資訊。  
  
-   **一次存取特定的 DBMS。** 例如，藉由呼叫 ODBC 函數來抓取資料的試算表，可能包含**driver**關鍵字來識別特定的驅動程式。 因為驅動程式名稱對任何擁有該驅動程式的使用者有意義，所以可以在這些使用者之間傳遞試算表。 如果試算表包含資料來源名稱，則每個使用者都必須建立相同的資料來源，才能使用試算表。  
  
-   **流覽系統，以尋找特定驅動程式可存取的所有資料庫。** 如需詳細資訊，請參閱本節稍後的[使用 SQLBrowseConnect 連接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。
