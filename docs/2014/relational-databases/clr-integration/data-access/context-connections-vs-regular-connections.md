---
title: 一般與內容連接 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8c2966244c8b23f58bf0762ae758ab298cc26c76
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037249"
---
# <a name="regular-vs-context-connections"></a>一般與內容連接
  如果您要連接到遠端伺服器，請務必使用正常連接而非內容連接。 如果您需要連接到執行預存程序或函數的相同伺服器，在大部分的情況下，請使用內容連接。 其優點包含可在相同的交易空間執行，以及不必重新驗證等等。  
  
 此外，使用內容連接通常會使效能更好，而且資源的使用量更少。 內容連接是一種僅限同處理序的連接，因此，它可以略過網路通訊協定與傳輸層來傳送 Transact-SQL 陳述式並接收結果，藉以「直接」與伺服器聯繫。 系統也會略過驗證處理序。 下圖顯示 `SqlClient` Managed 提供者的主要元件，以及使用正常連接或內容連接時，不同的元件分別如何與彼此互動。  
  
 ![內容和一般連接的程式碼路徑。](../../../database-engine/dev-guide/media/clrintdataaccess.gif "內容和一般連接的程式碼路徑。")  
  
 內容連接會遵循較短的程式碼路徑，並涉及較少的元件，因此，您可以預期會比在正常連接下，來回伺服器之要求和結果的速度還要快。 對於內容連接和正常連接，在伺服器上的查詢執行時間是相同的。  
  
 您有時候可能需要針對相同的伺服器開啟個別的正常連接。 比方說，有某些限制使用內容連接中所述[一般和內容連接的限制](context-connections-and-regular-connections-restrictions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [內容連接](context-connection.md)  
  
  