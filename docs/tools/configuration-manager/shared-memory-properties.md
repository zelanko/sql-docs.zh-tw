---
title: 共用記憶體屬性
description: 了解如何啟用或停用共用記憶體通訊協定，讓用戶端用來連線到在同一部電腦上執行的 SQL Server 執行個體。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 34a46a86e24e784ac7ab1426c843cfd2e2639dc3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481589"
---
# <a name="shared-memory-properties"></a>共用記憶體屬性
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  您可以使用 [共用記憶體屬性] 對話方塊上的 [通訊協定] 頁面來檢視與啟用共用記憶體通訊協定。 共用記憶體是使用上最簡單的通訊協定，而且不用設定任何設定。 因為使用共用記憶體通訊協定的用戶端，只能連線到在相同電腦上執行的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，所以不適用於大部分資料庫活動。 當您懷疑其他通訊協定的設定不正確時，請使用共用記憶體通訊協定進行疑難排解。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須重新啟動下列項目，才能啟用或停用通訊協定。  
  
## <a name="options"></a>選項。  
 **已啟用**  
 可能的值為 [是] 和 [否]。 根據預設，已啟用共用記憶體通訊協定。  
  
## <a name="see-also"></a>另請參閱  
 [選擇網路通訊協定](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))   
 [使用共用記憶體通訊協定建立有效的連接字串](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
