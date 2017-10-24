---
title: "記錄和資料流 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d11617fc364b3ce9f2c4f5b37623f4c74f968517
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="records-and-streams"></a>記錄和資料流
目前提供 ADO[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件做為存取資料來源，例如關聯式資料庫中的資訊的主要方法。 不過，某些提供者支援[記錄](../../../ado/reference/ado-api/record-object-ado.md)和[資料流](../../../ado/reference/ado-api/stream-object-ado.md)替代或互補的物件與資料提供者都可以管理的物件。 如需詳細資訊，在**記錄**行為，請參閱您的提供者文件。  
  
## <a name="records"></a>記錄  
 **記錄**物件基本上函式，一個資料列**資料錄集**s。 不過，**記錄**具有有限的功能相較於**資料錄集**，它們擁有不同的屬性和方法。中的資料來源**記錄**物件可以是從提供者會傳回一個資料列的命令。 使用**記錄**物件而非**資料錄集**接收從傳回一個資料列的查詢結果的物件就不具現化更複雜的額外負荷**資料錄集**物件。  
  
 **記錄**物件可以用於其他用途，特別是使用傳統的關聯式資料庫以外的資料來源的提供者這類[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 許多必須處理的資訊存在，為資料表在資料庫中，而訊息電子郵件系統和檔案在現代的檔案系統中。 **記錄**和**資料流**物件簡化存取儲存在關聯式資料庫以外的來源中的資訊。  
  
 **記錄**物件可代表和電子郵件系統中管理檔案系統 或 資料夾和 訊息中的目錄和檔案等資料。 針對這些用途，來源**記錄**可以是目前已開啟的資料列**資料錄集**，絕對 URL 或相對 URL 開啟搭配[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
 一般而言，**資料錄集**可用來代表容器或例如資料夾或目錄的階層中父代。 A**記錄**可用來傳回在父容器，例如檔案或文件中的一個節點的特定資訊。 主要原因**記錄**用來表示這種類型的資訊是這些資料來源的都是異質性。 這表示，每個**記錄**可能會有不同的集合和欄位數目。 傳統**資料錄集**包含從資料庫的資料列是同質性，這表示每個資料列有相同的數目和類型的欄位。  
  
 如需有關使用**記錄**處理這個異質資料，例如網際網路發行的提供者的提供者的物件，請參閱[ADO for Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
## <a name="streams"></a>資料流  
 **資料流**物件提供讀取、 寫入和管理位元組資料流的方式。 此位元組資料流可能是文字或二進位檔，並為大小只受限於系統資源。 一般而言，ADO**資料流**物件適用於下列用途：  
  
-   若要包含資料的**資料錄集**以 XML 格式儲存。 從這些 XML 資料流儲存**資料錄集**s 可以做為來源，當開啟新**資料錄集**。 如需詳細資訊，請參閱[資料流和持續性](../../../ado/guide/data/streams-and-persistence.md)。  
  
-   若要包含[CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md)要執行的提供者做為替代[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)。 例如，XML Updategram 可用做為來源對 Microsoft OLE DB 提供者命令適用於 SQL Server。  
  
-   以外的格式提供者接收結果**資料錄集**，例如從 Microsoft OLE DB Provider for SQL Server 的 XML 結果。 如需詳細資訊，請參閱[擷取成資料流的結果集](../../../ado/guide/data/retrieving-resultsets-into-streams.md)。  
  
-   若要包含的文字或位元組組成的檔案或訊息，常用的提供者，例如 Microsoft OLE DB Provider for Internet Publishing。 如需有關這種使用**資料流**物件，請參閱[ADO for Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
 A**資料流**可以在 開啟物件：  
  
-   以 URL 指定簡單的檔案。  
  
-   欄位的**記錄**或**資料錄集**包含**資料流**物件。  
  
-   預設資料流**記錄**或**資料錄集**物件，表示目錄或複合檔案。  
  
-   資源欄位，包含 URL 的簡單的檔案。  
  
-   完全沒有特定的來源。 在此情況下，**資料流**物件會在記憶體中開啟。 資料可以寫入和則儲存在另一個**資料流**或檔案。  
  
-   中的 BLOB 欄位**資料錄集**。  
  
 此章節包含下列主題。  
  
-   [資料流和持續性](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [命令資料流](../../../ado/guide/data/command-streams.md)  
  
-   [擷取結果集資料流](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [使用 ADO 的網際網路發行](../../../ado/guide/data/using-ado-for-internet-publishing.md)

