---
title: 記錄和資料流程 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4636df1451ba946b9a7bfb62e3d6775c35b1d6f3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924491"
---
# <a name="records-and-streams"></a>記錄和資料流
ADO 目前提供[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件做為存取資料來源（例如關係資料庫）中資訊的主要方法。 不過，某些提供者會支援[記錄](../../../ado/reference/ado-api/record-object-ado.md)和[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件做為替代物件或互補物件，並可從提供者運算元據。 如需**記錄**行為的詳細資訊，請參閱提供者的檔。  
  
## <a name="records"></a>記錄  
 **記錄**物件基本上會當做一個資料列**記錄集**來運作。 不過，相較于記錄**集**，**記錄**的功能有限，而且它們有不同的屬性和方法。**記錄**物件中的資料來源可以是命令，它會從提供者傳回一個資料列。 使用**記錄**物件，而不是**記錄集**物件，從傳回一列資料的查詢中接收結果，可避免具現化較複雜之**記錄集**物件的額外負荷。  
  
 **記錄**物件可以提供另一個用途，特別是傳統關係資料庫的提供者（例如， [Microsoft OLE DB 提供者用於網際網路發行](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)）。 必須處理的大部分資訊都存在，而不是資料庫中的資料表，而是在電子郵件系統中的訊息，以及新式檔案系統中的檔案。 **記錄**和**資料流程**物件有助於存取儲存在關係資料庫以外之來源中的資訊。  
  
 **記錄**物件可以代表和管理資料，例如檔案系統中的目錄和檔案，或電子郵件系統中的資料夾和訊息。 基於這些目的，**記錄**的來源可以是開啟之**記錄集**的目前資料列、絕對 URL，或與開啟的[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件結合的相對 URL。  
  
 通常，**記錄集**可以用來代表階層中的容器或父系，例如資料夾或目錄。 **記錄**可以用來傳回父容器中某個節點的特定資訊，例如檔案或檔。 主要原因**記錄**是用來表示這種類型的資訊，這是因為這些資料來源是異類的。 這表示每筆**記錄**可能會有不同的設定和數目的欄位。 包含資料庫中資料列的傳統**記錄集**是同質的，這表示每個資料列都有相同數目和類型的欄位。  
  
 如需使用**記錄**物件來處理來自網際網路發行提供者等提供者之異質資料的詳細資訊，請參閱[使用 ADO 進行網際網路發佈](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
## <a name="streams"></a>資料流  
 **Stream**物件提供讀取、寫入和管理位元組資料流程的方法。 這個位元組資料流程可以是文字或二進位檔，而且只有系統資源的大小限制。 一般來說，ADO**資料流程**物件是用於下列用途：  
  
-   包含以 XML 格式儲存的**記錄集**資料。 這些來自已儲存**記錄集**的 XML 資料流程，在開啟新的**記錄集**時，可以當做來源使用。 如需詳細資訊，請參閱[資料流程和持續](../../../ado/guide/data/streams-and-persistence.md)性。  
  
-   包含要對提供者執行的[CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md) ，以做為[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)的替代方法。 例如，您可以使用 XML Updategram 做為適用于 SQL Server 的 Microsoft OLE DB 提供者之命令的來源。  
  
-   以**記錄集**以外的格式接收來自提供者的結果，例如適用于 SQL Server Microsoft OLE DB 提供者的 XML 結果。 如需詳細資訊，請參閱將結果集抓取[到資料流程](../../../ado/guide/data/retrieving-resultsets-into-streams.md)。  
  
-   若要包含組成檔案或訊息的文字或位元組，通常會搭配提供者（例如 Microsoft OLE DB 提供者）用於網際網路發行。 如需有關這種**資料流程**物件使用方式的詳細資訊，請參閱[使用 ADO 進行網際網路發佈](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
 **資料流程**物件可以在上開啟：  
  
-   以 URL 指定的簡單檔案。  
  
-   包含**資料流程**物件之**記錄**或**記錄集**的欄位。  
  
-   代表目錄或複合檔案的**記錄**或**記錄集**物件的預設資料流程。  
  
-   資源欄位，其中包含簡單檔案的 URL。  
  
-   完全沒有特定來源。 在此情況下，**資料流程**物件會在記憶體中開啟。 資料可以寫入其中，然後儲存在另一個**資料流程**或檔案中。  
  
-   **記錄集中**的 BLOB 欄位。  
  
 此章節包含下列主題。  
  
-   [資料流和保存](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [命令資料流](../../../ado/guide/data/command-streams.md)  
  
-   [將結果集擷取為資料流](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [使用 ADO 進行網際網路發佈](../../../ado/guide/data/using-ado-for-internet-publishing.md)
