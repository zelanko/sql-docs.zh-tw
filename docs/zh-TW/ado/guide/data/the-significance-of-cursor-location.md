---
title: 資料指標位置的重要性 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b979966c2a879ea41ff559a6b554efdbf11ca3d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="the-significance-of-cursor-location"></a>資料指標位置的精確度倍數
每個資料指標使用的暫存資源，來保留資料。 這些資源可以是記憶體、 磁碟分頁檔中，暫存磁碟檔案或甚至暫時儲存在資料庫中。 資料指標稱為*用戶端*時這些資源位於用戶端電腦上的資料指標。 資料指標稱為*伺服器端*時這些資源位於伺服器上的資料指標。  
  
## <a name="client-side-cursors"></a>用戶端資料指標  
 在 ADO 中，用戶端資料指標所使用呼叫**adUseClient CursorLocationEnum。** 使用非索引鍵集用戶端資料指標，伺服器會傳送整個結果集在網路上用戶端電腦。 用戶端電腦提供並管理資料指標和結果集所需的暫存資源。 用戶端應用程式可以瀏覽整個結果集來判斷它需要哪些資料列。  
  
 靜態和索引鍵集導向的用戶端資料指標可能很大的負擔，您的工作站上，如果它們包含太多資料列。 當所有資料指標程式庫能夠建置數千個資料列的資料指標時，設計來擷取這類大型資料列集的應用程式可能會無限期地執行狀況不佳。 當然也有例外狀況。 對於某些應用程式中，大型的用戶端資料指標可能非常恰當，效能可能不會產生問題。  
  
 用戶端資料指標的一個明顯的好處是快速的回應。 結果集已下載至用戶端電腦之後，瀏覽資料列是非常快速。 您的應用程式是通常更具擴充性與用戶端資料指標，因為每個個別的用戶端和伺服器上找不到放置游標的資源需求。  
  
## <a name="server-side-cursors"></a>伺服器端資料指標  
 在 ADO 中，由伺服器端資料指標使用呼叫**adUseServer CursorLocationEnum。** 使用伺服器端資料指標，伺服器會管理結果集使用提供的伺服器電腦的資源。 伺服器端資料指標會傳回要求的資料在網路上。 這種類型的資料指標有時候可以提供較佳的效能比用戶端資料指標，特別是在網路流量過大時問題。  
  
 不過，請務必指出伺服器端資料指標是 — 至少暫時如此 — 針對每個作用中的用戶端耗用寶貴的伺服器資源。 您必須據此規劃以確保您的伺服器硬體能夠管理所有作用中用戶端所要求的伺服器端資料指標。 此外，因為它提供只有單一資料列存取伺服器端資料指標可能會很慢，沒有可用的批次資料指標。  
  
 伺服器端資料指標是當插入、 更新或刪除資料錄時很有用。 與伺服器端資料指標，在相同的連接上可以有多個作用中陳述式。
