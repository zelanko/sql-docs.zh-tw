---
title: 預設追蹤記錄檔已停用 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c27761e6-75ed-4ee4-a236-0cbc42e500a1
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ff8c58652c33de32f756528e7fd8a372032112f9
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43816216"
---
# <a name="default-trace-log-files-disabled"></a>預設追蹤記錄檔已停用
  此規則會檢查 sp_configure 預存程序 default trace enabled 選項的值，以判斷預設追蹤是否設定為 ON (1) 或 OFF (0)。 當啟用這個選項時，預設追蹤會提供有關組態及 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]之 DDL 變更的資訊。 在某些情況下，當客戶和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客戶服務及支援中心在排除 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的問題時，這項資訊對於他們很有幫助。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 使用 sp_configure 預存程序，將 default trace enabled 設定為 1 的值來啟用追蹤。  
  
## <a name="for-more-information"></a>詳細資訊  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
