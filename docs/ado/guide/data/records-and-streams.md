---
title: 記錄和資料流 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b9e26930db786b986fd1f4ba633e2cc5953f3df3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681356"
---
# <a name="records-and-streams"></a>記錄和資料流
目前提供 ADO[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件做為存取資料來源，例如關聯式資料庫中的資訊的主要方法。 不過，某些提供者支援[記錄](../../../ado/reference/ado-api/record-object-ado.md)並[Stream](../../../ado/reference/ado-api/stream-object-ado.md)做為替代或互補的物件與提供者的資料都可以操作的物件。 如需詳細資訊**記錄**行為，請參閱您的提供者文件。  
  
## <a name="records"></a>記錄  
 **資料錄**物件基本上是函式，一個資料列**資料錄集**s。 不過，**記錄**有限的功能相較於**資料錄集**，它們擁有不同的屬性和方法。中的資料來源**記錄**物件可以是命令，這個命令會從提供者會傳回一個資料列。 使用**記錄**物件而非**Recordset**物件接收的查詢會傳回一個資料列的結果就不具現化更複雜的額外負荷**資料錄集**物件。  
  
 **資料錄**物件可以用於其他用途，特別是使用傳統的關聯式資料庫以外的資料來源的提供者這類[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 大部分必須處理的資訊存在，無法為資料表在資料庫中，而訊息電子郵件系統和檔案在現代的檔案系統中。 **記錄**並**Stream**物件簡化存取儲存在關聯式資料庫以外的來源中的資訊。  
  
 **記錄**物件可代表和檔案系統或資料夾，而訊息中的資料，例如目錄和檔案管理電子郵件系統中。 基於上述目的，針對來源**記錄**可以是已開啟的目前資料列**資料錄集**，絕對 URL 或開啟搭配的相對 URL[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
 通常**資料錄集**可用來代表容器或階層，例如資料夾或目錄中的父代。 A**記錄**可用來傳回父容器，例如檔案或文件中的一個節點的特定資訊。 主要的原因**記錄**用來表示這種類型的資訊是這些來源的資料都是異質性。 這表示，每個**記錄**可能會有不同的集合和欄位數目。 傳統**資料錄集**從資料庫所包含的資料列都同質性，這表示每個資料列具有相同數目和類型的欄位。  
  
 如需使用詳細資訊**記錄**物件來處理此提供者，例如網際網路發佈提供者的異質資料，請參閱[使用的 ADO for Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
## <a name="streams"></a>資料流  
 **Stream**物件會提供方法來讀取、 寫入及管理位元組資料流。 此位元組資料流可以是文字或二進位檔，大小只受限於系統資源。 一般而言，ADO **Stream**物件用於下列用途：  
  
-   若要包含的資料**資料錄集**以 XML 格式儲存。 從這些 XML 資料流儲存**Recordset**開啟新時，可以做為來源使用 s**資料錄集**。 如需詳細資訊，請參閱 <<c0> [ 資料流和保存](../../../ado/guide/data/streams-and-persistence.md)。  
  
-   若要包含[CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md)執行的提供者，做為替代[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)。 例如，XML Updategram 可用來當做來源對 Microsoft OLE DB 提供者命令適用於 SQL Server。  
  
-   從以格式提供者接收結果時，也將以外**資料錄集**，例如來自 Microsoft OLE DB Provider for SQL Server 的 XML 結果。 如需詳細資訊，請參閱 <<c0> [ 擷取到資料流的結果集](../../../ado/guide/data/retrieving-resultsets-into-streams.md)。  
  
-   若要包含的文字或位元組組成的檔案或訊息，常用的提供者，例如 Microsoft OLE DB Provider for Internet Publishing。 如需有關此善用**Stream**物件，請參閱[使用的 ADO for Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
 A **Stream**物件能上，開啟：  
  
-   以 URL 指定簡單的檔案。  
  
-   欄位**記錄**或是**Recordset**包含**Stream**物件。  
  
-   預設資料流**記錄**或是**資料錄集**物件，表示目錄或複合檔案。  
  
-   資源欄位，包含 URL 的簡單的檔案。  
  
-   完全沒有特定的來源。 在此情況下， **Stream**開啟物件在記憶體中。 資料可以寫入至其中，則儲存在另一個**Stream**或檔案。  
  
-   中的 BLOB 欄位**資料錄集**。  
  
 此章節包含下列主題。  
  
-   [資料流和保存](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [命令資料流](../../../ado/guide/data/command-streams.md)  
  
-   [將結果集擷取為資料流](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [使用 ADO 進行網際網路發佈](../../../ado/guide/data/using-ado-for-internet-publishing.md)
