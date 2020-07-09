---
title: 網路封包大小不應超過 8060 個位元組 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7800bf2c9724cec7ba8100e7268e1760e39d3afe
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85785065"
---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>網路封包大小不應超過 8060 個位元組
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  如果為 sp_configure 'network packet size' 指定的值或是任何已登入使用者的網路封包大小超過 8060 個位元組， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會執行不同的記憶體配置作業。 這會造成未保留給緩衝集區的處理序虛擬位置空間增加。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 網路封包大小不應超過 8060 個位元組。  
  
## <a name="for-more-information"></a>詳細資訊  
 [Microsoft 知識庫文章 903002](https://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
