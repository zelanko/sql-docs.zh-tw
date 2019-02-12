---
title: 升級查閱轉換 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation and upgrading
- upgrading caching for Lookup transformation
- upgrading Lookup transformation
ms.assetid: d9b2c281-91ee-4e20-bdf0-0cd77d4a4241
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 159779bc43edf7d30182e86aee545e6e9db8135a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032369"
---
# <a name="upgrade-lookup-transformations"></a>升級查閱轉換
  當您從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時，請考慮修改封裝，以利用查閱轉換中的新功能。 此轉換支援 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 中所提供的快取類型與資料輸出選項。 如需有關其他快取和資料輸出，請參閱[查閱 」 轉換](../../integration-services/data-flow/transformations/lookup-transformation.md)。  
  
 在 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 中，可用的快取類型包括完整快取、部分快取和無快取。 在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中，您可以將查閱轉換設定為使用其中一種快取類型。 如需有關如何實作部分快取或無快取，請參閱 <<c0> [ 以沒有快取或部分快取模式實作查閱](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)。 如需有關如何實作完整快取的資訊，請參閱 <<c0> [ 快取連接管理員中使用完整快取模式實作查閱轉換](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)和[Full Cache Mode Using OLE 中實作查閱轉換DB 連接管理員](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)。  
  
 在 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 中，查閱轉換具有輸入、輸出和錯誤輸出。 輸出會處理在參考資料集中具有相符項目的輸入資料列。 沒有相符項目的輸入資料列會被視為錯誤，而且可能會重新導向至錯誤輸出。 在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中，查閱轉換有兩個輸出：相符結果輸出和無相符結果輸出。  
  
 根據預設，當您執行在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中建立的查閱轉換時，[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 會將沒有相符項目的資料列視為錯誤，而且讓您將這些資料列重新導向至錯誤輸出。 您可以選擇設定查閱轉換，以便將這些資料列視為非錯誤，然後將這些資料列重新導向至無相符結果輸出。  
  
 如需詳細資訊，請參閱 <<c0> [ 查閱轉換編輯器&#40;一般頁面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [Lookup Transformation](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
