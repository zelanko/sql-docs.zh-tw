---
title: 升級查閱轉換 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Lookup transformation and upgrading
- upgrading caching for Lookup transformation
- upgrading Lookup transformation
ms.assetid: d9b2c281-91ee-4e20-bdf0-0cd77d4a4241
caps.latest.revision: 16
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 214d915f16f15e81fe4fabbb44dd34f665fb5942
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031550"
---
# <a name="upgrade-lookup-transformations"></a>升級查閱轉換
  當您從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時，請考慮修改封裝，以利用查閱轉換中的新功能。 此轉換支援 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 中所提供的快取類型與資料輸出選項。 如需有關其他快取和資料輸出，請參閱[查閱轉換](../../integration-services/data-flow/transformations/lookup-transformation.md)。  
  
 在 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 中，可用的快取類型包括完整快取、部分快取和無快取。 在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中，您可以將查閱轉換設定為使用其中一種快取類型。 如需有關如何實作部分快取或沒有快取，請參閱[以沒有快取或部分快取模式實作查閱](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)。 如需如何實作完整快取資訊，請參閱[完整快取模式中使用快取連接管理員實作查閱轉換](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)和[完整快取模式中使用的 OLE 實作查閱轉換DB 連接管理員](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)。  
  
 在 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 中，查閱轉換具有輸入、輸出和錯誤輸出。 輸出會處理在參考資料集中具有相符項目的輸入資料列。 沒有相符項目的輸入資料列會被視為錯誤，而且可能會重新導向至錯誤輸出。 在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中，查閱轉換有兩個輸出：相符結果輸出和無相符結果輸出。  
  
 根據預設，當您執行在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中建立的查閱轉換時，[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 會將沒有相符項目的資料列視為錯誤，而且讓您將這些資料列重新導向至錯誤輸出。 您可以選擇設定查閱轉換，以便將這些資料列視為非錯誤，然後將這些資料列重新導向至無相符結果輸出。  
  
 如需詳細資訊，請參閱[查閱轉換編輯器&#40;[一般] 頁面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)。  
  
## <a name="see-also"></a>另請參閱  
 [查閱轉換](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  