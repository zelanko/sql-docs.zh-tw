---
title: 雙向異動複寫 | Microsoft Docs
description: 雙向異動複寫可讓兩部伺服器交換變更。 每部伺服器都會發佈資料，並訂閱另一部伺服器中的發行集。
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: f8a22b04834cc80b3b64cf7384bc6fe97d2f0571
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97406275"
---
# <a name="bidirectional-transactional-replication"></a>雙向異動複寫
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  雙向異動複寫是一種特殊的異動複寫拓撲，它可讓兩台伺服器彼此之間交換變更：每台伺服器都會發行資料，然後向發行集訂閱另一台伺服器上相同的資料。 [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 的`@loopback_detection` 參數已設定為 TRUE，以確定變更僅傳送到訂閱者而不會將變更傳回給發行者。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 及更新的版本中，點對點異動複寫也支援此拓撲，但雙向複寫可提升效能。  
  
## <a name="see-also"></a>另請參閱  
 [@loopback_detection](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
