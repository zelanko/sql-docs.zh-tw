---
title: 順向資料指標 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee3d8a80598e3f41bd6bfaf9a493639ee36cd3ee
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47802836"
---
# <a name="forward-only-cursors"></a>順向資料指標
典型的預設資料指標類型，稱為 「 順向 （或非可捲動） 資料指標，可以透過結果集只會順向移動的。 順向資料指標不支援捲動 （向前及向後移動結果集中的能力）;它只支援從一開始提取資料列，結果集的結尾。 與某些順向資料指標 (例如使用 SQL Server 資料指標程式庫)，則所有 insert、 update 和 delete 陳述式所做的目前使用者 （或其他使用者所認可的） 影響結果集中的資料列是可見的因為提取資料列。 因為無法往回捲動資料指標，不過，提取資料列之後，在資料庫中的資料列所做的變更不會顯示透過資料指標。  
  
 處理目前的資料列的資料之後，順向資料指標就會釋放已用來保存該資料的資源。 順向資料指標是動態的根據預設，這表示，處理目前的資料列時，會偵測到的所有變更。 這提供更快速的資料指標開啟，並可將結果集顯示基礎資料表所做的更新。  
  
 雖然順向資料指標不支援向後捲動，您的應用程式可以傳回結果集關閉並重新開啟資料指標的開頭。 這是有效的方法，才能使用少量的資料。 或者，您的應用程式無法讀取結果集一次，快取在本機的資料，然後瀏覽本機資料快取。  
  
 如果您的應用程式不需要捲動的結果集，順向資料指標是使用最少的額外負荷快速擷取資料的最佳方式。 使用  **adOpenForwardOnly CursorTypeEnum**來指出您想要使用順向資料指標在 ADO 中。  
  
## <a name="see-also"></a>另請參閱  
 [靜態資料指標](../../../ado/guide/data/static-cursors.md)   
 [索引鍵集資料指標](../../../ado/guide/data/keyset-cursors.md)   
 [動態資料指標](../../../ado/guide/data/dynamic-cursors.md)
