---
description: 順向資料指標
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e26b3f364595adea7e1eadc65114bffb19db2639
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806822"
---
# <a name="forward-only-cursors"></a>順向資料指標
一般預設資料指標類型（稱為順向 (或非可滾動的) 資料指標）只能在結果集中向前移動。 順向資料指標不支援滾動 (在結果集中向前及向後移動的能力) ;它僅支援從開始到結果集的結尾提取資料列。 使用某些順向資料指標 (例如 SQL Server 資料指標程式庫) ，目前使用者所做的所有插入、更新和刪除語句 (或由其他使用者所認可，) 會在提取資料列時顯示結果集內的資料列。 不過，由於無法反向捲動資料指標，因此擷取資料列之後對資料庫中資料列所進行的變更，都無法經由資料指標看見。  
  
 處理目前資料列的資料之後，順向資料指標會釋放用來保存該資料的資源。 順向資料指標預設是動態的，這表示當處理目前的資料列時會偵測到所有變更。 這會加速資料指標的開啟，並讓結果集顯示對基礎資料表所做的更新。  
  
 雖然順向資料指標不支援回溯滾動，但您的應用程式可以藉由關閉並重新開啟資料指標，來返回結果集的開頭。 這是處理少量資料的有效方式。 或者，您的應用程式可以讀取結果集一次，在本機快取資料，然後流覽本機資料快取。  
  
 如果您的應用程式不需要在結果集中進行滾動，順向資料指標是以最少量的額外負荷快速取出資料的最佳方式。 使用 **AdOpenForwardOnly CursorTypeEnum** 來指出您想要在 ADO 中使用順向資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [靜態資料指標](./static-cursors.md)   
 [索引鍵集資料指標](./keyset-cursors.md)   
 [動態資料指標](./dynamic-cursors.md)