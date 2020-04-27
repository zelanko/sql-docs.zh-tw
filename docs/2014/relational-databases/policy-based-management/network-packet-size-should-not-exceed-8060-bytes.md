---
title: 網路封包大小不應超過 8060 個位元組 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1d66ba3298b2346e2ec139f27ec53d6104ad0ac9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62625808"
---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>網路封包大小不應超過 8060 個位元組
  如果為 sp_configure 'network packet size' 指定的值或是任何已登入使用者的網路封包大小超過 8060 個位元組， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會執行不同的記憶體配置作業。 這會造成未保留給緩衝集區的處理序虛擬位置空間增加。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 網路封包大小不應超過 8060 個位元組。  
  
## <a name="for-more-information"></a>詳細資訊  
 [Microsoft 知識庫文章 903002](https://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
