---
title: "共用記憶體屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 431107cdbdfdcfd97027500e77ea3cf35a989957
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="shared-memory-properties"></a>共用記憶體屬性
  您可以使用 [共用記憶體屬性] 對話方塊上的 [通訊協定] 頁面來檢視與啟用共用記憶體通訊協定。 共用記憶體是使用上最簡單的通訊協定，而且不用設定任何設定。 因為使用共用記憶體通訊協定的用戶端，只能連接到在相同電腦上執行的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，所以不適用於大部分資料庫活動。 當您懷疑其他通訊協定的設定不正確時，請使用共用記憶體通訊協定進行疑難排解。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須重新啟動下列項目，才能啟用或停用通訊協定。  
  
## <a name="options"></a>選項。  
 **已啟用**  
 可能的值為 [是] 和 [否]。 根據預設，已啟用共用記憶體通訊協定。  
  
## <a name="see-also"></a>另請參閱  
 [選擇網路通訊協定](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [使用共用記憶體通訊協定建立有效的連接字串](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  

