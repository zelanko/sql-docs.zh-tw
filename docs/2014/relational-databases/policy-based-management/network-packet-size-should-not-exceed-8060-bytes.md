---
title: 網路封包大小不應超過 8060 個位元組 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b7af9200587423dd8229ce699ed036cc4ce24f1f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303678"
---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>網路封包大小不應超過 8060 個位元組
  如果為 sp_configure 'network packet size' 指定的值或是任何已登入使用者的網路封包大小超過 8060 個位元組， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會執行不同的記憶體配置作業。 這會造成未保留給緩衝集區的處理序虛擬位置空間增加。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 網路封包大小不應超過 8060 個位元組。  
  
## <a name="for-more-information"></a>詳細資訊  
 [Microsoft 知識庫文章 903002](http://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
