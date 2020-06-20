---
title: 共用記憶體屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6275215afdb6de3aa134dbffe74aa22b9e7b6f5d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054480"
---
# <a name="shared-memory-properties"></a>共用記憶體屬性
  您可以使用 [共用記憶體屬性] 對話方塊上的 [通訊協定] 頁面來檢視與啟用共用記憶體通訊協定。 共用記憶體是使用上最簡單的通訊協定，而且不用設定任何設定。 因為使用共用記憶體通訊協定的用戶端，只能連線到在相同電腦上執行的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，所以不適用於大部分資料庫活動。 當您懷疑其他通訊協定的設定不正確時，請使用共用記憶體通訊協定進行疑難排解。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須重新啟動下列項目，才能啟用或停用通訊協定。  
  
## <a name="options"></a>選項。  
 **已啟用**  
 可能的值為 [是]  和 [否]  。 根據預設，已啟用共用記憶體通訊協定。  
  
## <a name="see-also"></a>另請參閱  
 [選擇網路通訊協定](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [使用共用記憶體通訊協定建立有效的連接字串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
