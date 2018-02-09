---
title: "順向資料指標 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b84ab8335e94adecf130fd2301f697a02eceee37
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="forward-only-cursors"></a>順向資料指標
典型的預設資料指標類型，稱為 「 順向 （或非可捲動） 資料指標，可僅向前移動的結果集。 順向資料指標不支援捲動 （向前及向後移動結果集中的能力）。它只支援從一開始提取資料列結果集的結尾。 與某些順向資料指標 (例如與 SQL Server 資料指標程式庫)，則所有 insert、 update 和 delete 陳述式所做的目前使用者 （或其他使用者所認可），會影響結果集中的資料列都是可見的提取資料列。 因為無法逆向捲動資料指標，不過，提取資料列之後，資料庫中的資料列所做的變更都無法看見透過資料指標。  
  
 處理目前的資料列的資料之後，順向資料指標就會釋放已用來保存該資料的資源。 順向資料指標是動態的根據預設，這表示，處理目前的資料列時，會偵測到的所有變更。 這提供更快速的資料指標開啟，並可將結果集顯示基礎資料表所做的更新。  
  
 雖然順向資料指標不支援向後捲動，您的應用程式可以傳回結果集關閉並重新開啟資料指標的開頭。 這是有效的方式，來使用少量的資料。 或者，您的應用程式無法讀取結果集一次、 快取資料在本機，，然後瀏覽本機資料快取。  
  
 如果您的應用程式不需要捲動的結果集，順向資料指標會是負擔的最佳的方式來擷取資料，快速地以最少。 使用**adOpenForwardOnly CursorTypeEnum**來指出您想要使用順向資料指標在 ADO 中。  
  
## <a name="see-also"></a>另請參閱  
 [靜態資料指標](../../../ado/guide/data/static-cursors.md)   
 [索引鍵集資料指標](../../../ado/guide/data/keyset-cursors.md)   
 [動態資料指標](../../../ado/guide/data/dynamic-cursors.md)
