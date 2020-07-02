---
title: 一般與內容連接 |Microsoft Docs
description: 在 SQL Server 中，有時候您必須使用 Transact-sql 語句的一般連接，但內容連接可提供效能和資源使用方式的優點。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
author: rothja
ms.author: jroth
ms.openlocfilehash: 6417a0121a7e290d711690fb0150fdbe908827dd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637517"
---
# <a name="context-connections-vs-regular-connections"></a>內容連接與一般連接的比較
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  如果您要連接到遠端伺服器，請務必使用正常連接而非內容連接。 如果您需要連接到執行預存程序或函數的相同伺服器，在大部分的情況下，請使用內容連接。 其優點包含可在相同的交易空間執行，以及不必重新驗證等等。  
  
 此外，使用內容連接通常會使效能更好，而且資源的使用量更少。 內容連線是一個同進程的連線，因此它可以藉由略過網路通訊協定和傳輸層來傳送 Transact-sql 語句並接收結果，以「直接」連線到伺服器。 系統也會略過驗證處理序。 下圖顯示**SqlClient**受控提供者的主要元件，以及不同元件在使用一般連接時與彼此互動的方式，以及使用內容連接的時機。  
  
 ![內容和一般連接的程式碼路徑。](../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "內容和一般連接的程式碼路徑。")  
  
 內容連接會遵循較短的程式碼路徑，並涉及較少的元件，因此，您可以預期會比在正常連接下，來回伺服器之要求和結果的速度還要快。 對於內容連接和正常連接，在伺服器上的查詢執行時間是相同的。  
  
 您有時候可能需要針對相同的伺服器開啟個別的正常連接。 例如，使用內容連接有一些限制，如[一般和內容連接的限制](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)中所述。  
  
## <a name="see-also"></a>另請參閱  
 [內容連接](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
