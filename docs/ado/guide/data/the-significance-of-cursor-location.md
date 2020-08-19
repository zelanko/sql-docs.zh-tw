---
description: 資料指標位置的精確度
title: 資料指標位置的重要性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
author: rothja
ms.author: jroth
ms.openlocfilehash: acfb19f341bef22a9922e075d144026b9ef5f29d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452720"
---
# <a name="the-significance-of-cursor-location"></a>資料指標位置的精確度
每個資料指標都會使用暫存資源來保存其資料。 這些資源可以是記憶體、磁片分頁檔案、暫存磁片檔案，甚至是資料庫中的暫存儲存體。 當這些資源位於用戶端電腦上時，會將資料指標稱為 *客戶* 端資料指標。 當這些資源位於伺服器上時，資料指標就稱為 *伺服器端* 資料指標。  
  
## <a name="client-side-cursors"></a>用戶端資料指標  
 在 ADO 中，使用**AdUseClient CursorLocationEnum**呼叫用戶端資料指標。 使用非索引鍵集用戶端資料指標時，伺服器會透過網路將整個結果集傳送到用戶端電腦。 用戶端電腦會提供和管理資料指標和結果集所需的暫存資源。 用戶端應用程式可以流覽整個結果集，以決定所需的資料列。  
  
 如果靜態和索引鍵集驅動用戶端資料指標包含太多資料列，可能會在您的工作站上造成大量負載。 雖然所有資料指標程式庫都能夠建立具有上千個數據列的資料指標，但設計來提取這類大型資料列集的應用程式可能會執行得不佳。 當然有一些例外狀況。 對於某些應用程式而言，大型用戶端資料指標可能完全適當，且效能可能不會是問題。  
  
 用戶端資料指標的一個明顯優點是快速回應。 將結果集下載到用戶端電腦之後，流覽資料列的速度非常快。 因為資料指標的資源需求是放置在每個不同的用戶端，而不是在伺服器上，所以您的應用程式通常更能以用戶端資料指標進行擴充。  
  
## <a name="server-side-cursors"></a>伺服器端資料指標  
 在 ADO 中，使用**AdUseServer CursorLocationEnum**呼叫伺服器端資料指標。 使用伺服器端資料指標時，伺服器會使用伺服器電腦所提供的資源來管理結果集。 伺服器端資料指標只會傳回透過網路所要求的資料。 這種類型的資料指標有時可以提供比用戶端資料指標更佳的效能，特別是在網路流量過大的情況下。  
  
 不過，請務必指出伺服器端的資料指標至少為每個作用中用戶端的每個使用中的寶貴伺服器資源。 您必須據此進行規劃，以確保您的伺服器硬體能夠管理作用中用戶端所要求的所有伺服器端資料指標。 此外，伺服器端資料指標可能會變慢，因為它只提供單一資料列存取-沒有可用的批次資料指標。  
  
 在插入、更新或刪除記錄時，伺服器端資料指標很有用。 使用伺服器端資料指標，您可以在相同的連接上擁有多個作用中語句。
