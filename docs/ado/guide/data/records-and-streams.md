---
description: 記錄和資料流
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8afaae4221c57a7f7d832c34f0a374981e081cf6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452980"
---
# <a name="records-and-streams"></a>記錄和資料流
ADO 目前提供 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件作為存取資料來源中資訊的主要方法，例如關係資料庫。 不過，某些提供者支援 [記錄](../../../ado/reference/ado-api/record-object-ado.md) 和 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md) 物件，做為替代物件或可操作提供者資料的互補物件。 如需 **記錄** 行為的詳細資訊，請參閱提供者的檔。  
  
## <a name="records"></a>記錄  
 **記錄** 物件基本上是做為單一資料列 **記錄集**的功能。 不過，相較于記錄**集**，**記錄**的功能有限，而且具有不同的屬性和方法。**記錄**物件中的資料來源可以是從提供者傳回一列資料的命令。 使用 **Record** 物件（而不是 **記錄集** 物件）從傳回一列資料的查詢接收結果，可避免將更複雜的 **記錄集** 物件具現化的額外負荷。  
  
 **記錄** 物件可提供其他用途，特別是傳統關係資料庫以外的資料來源提供者，例如 [Microsoft OLE DB Provider for Internet 發行](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 大部分必須處理的資訊都存在，而不是資料庫中的資料表，而是在新式檔案系統的電子郵件系統和檔案中的訊息。 **記錄**和**資料流程**物件有助於存取儲存在關係資料庫以外之來源中的資訊。  
  
 **記錄**物件可以表示和管理資料，例如檔案系統中的目錄和檔案，或電子郵件系統中的資料夾和訊息。 基於這些目的， **記錄** 的來源可以是開啟之 **記錄集**的目前資料列、絕對 URL，或是與開啟的 [連接](../../../ado/reference/ado-api/connection-object-ado.md) 物件結合的相對 URL。  
  
 通常， **記錄集** 可以用來代表階層中的容器或父系，例如資料夾或目錄。 **記錄**可以用來傳回父容器中某個節點的特定資訊，例如檔案或檔。 主要原因 **記錄** 用來表示這類資訊，就是這些資料來源都是異類的。 這表示每筆 **記錄** 可能會有不同的設定和欄位數目。 包含資料庫中資料列的傳統 **記錄集** 是同質的，這表示每個資料列都有相同的欄位數目和類型。  
  
 如需使用 **記錄** 物件來處理來自提供者（例如網際網路發佈提供者）的這類異質資料的詳細資訊，請參閱 [使用 ADO 進行網際網路發佈](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
## <a name="streams"></a>串流  
 **Stream**物件提供讀取、寫入和管理位元組資料流程的方法。 此位元組資料流程可以是文字或二進位檔，且僅限系統資源的大小。 一般情況下，ADO **資料流程** 物件是用於下列用途：  
  
-   包含以 XML 格式儲存之 **記錄集** 的資料。 開啟新的**記錄**集時，可以使用已儲存**記錄集**的這些 XML 資料流程作為來源。 如需詳細資訊，請參閱 [資料流程和持續](../../../ado/guide/data/streams-and-persistence.md)性。  
  
-   包含要對提供者執行的 [CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md) ，做為 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)的替代方案。 例如，XML Updategram 可用來做為適用于 SQL Server 的 Microsoft OLE DB 提供者之命令的來源。  
  
-   以 **記錄集**以外的格式接收來自提供者的結果，例如來自 Microsoft OLE DB provider for SQL SERVER 的 XML 結果。 如需詳細資訊，請參閱將 [結果集取出至資料流程](../../../ado/guide/data/retrieving-resultsets-into-streams.md)。  
  
-   若要包含組成檔案或訊息的文字或位元組，通常會與提供者（例如 Microsoft OLE DB Provider for Internet 發行）搭配使用。 如需這種 **資料流程** 物件用法的詳細資訊，請參閱 [使用 ADO 進行網際網路發佈](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
 **資料流程**物件可以開啟：  
  
-   以 URL 指定的簡單檔案。  
  
-   包含**資料流程**物件之**記錄**或**記錄集**的欄位。  
  
-   **記錄**或**記錄集**物件的預設資料流程，代表目錄或複合檔案。  
  
-   資源欄位，包含簡單檔案的 URL。  
  
-   沒有特定的來源。 在此情況下， **資料流程** 物件會在記憶體中開啟。 您可以將資料寫入其中，然後儲存在另一個 **資料流程** 或檔案中。  
  
-   **記錄集中**的 BLOB 欄位。  
  
 此章節包含下列主題。  
  
-   [資料流和保存](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [命令資料流](../../../ado/guide/data/command-streams.md)  
  
-   [將結果集擷取為資料流](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [使用 ADO 進行網際網路發佈](../../../ado/guide/data/using-ado-for-internet-publishing.md)
