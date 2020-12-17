---
title: 用戶端通訊協定 - 具名管道內容 (通訊協定索引標籤)
description: 了解如何在 SQL Server 組態管理員中檢視或修改預設管道的描述。 了解如何連線到不同管道。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 6e637bb0dd5979e5149ef70cba59ed8a4ac7f583
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463880"
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>用戶端通訊協定 - 具名管道內容 (通訊協定索引標籤)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中，使用 [具名管道屬性] 對話方塊的 [通訊協定] 索引標籤來檢視或修改預設管道的描述。 若要連接到其他管道，請在 **[預設管道]** 方塊內輸入管道名稱。 如需有關連接字串的詳細資訊，請參閱＜ [Creating a Valid Connection String Using Named Pipes](/previous-versions/sql/sql-server-2016/ms189307(v=sql.130))＞。  
  
## <a name="options"></a>選項。  
 **[預設管道]**  
 指定「具名管道網路」程式庫嘗試連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的目標執行個體時要使用的預設管道。 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會接聽： `\\.\pipe\sql\query`  
  
 若要連接到預設管道，請輸入 `sql\query`  
  
 **已啟用**  
 可能的值為 [是] 和 [否]。  
  
## <a name="see-also"></a>另請參閱  
 [選擇網路通訊協定](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))  
  
