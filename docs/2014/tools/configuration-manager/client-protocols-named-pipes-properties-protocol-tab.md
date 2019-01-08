---
title: 用戶端通訊協定 - 具名管道屬性 ([通訊協定] 索引標籤) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fe7bb05afc8e0814ddb3d872a810759aae2a678
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52746841"
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>用戶端通訊協定 - 具名管道內容 (通訊協定索引標籤)
  在「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」中，使用 **[Named Pipes 內容]** 對話方塊的 **[通訊協定]** 索引標籤來檢視或修改預設管道的描述。 若要連接到其他管道，請在 **[預設管道]** 方塊內輸入管道名稱。 如需有關連接字串的詳細資訊，請參閱＜ [Creating a Valid Connection String Using Named Pipes](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)＞。  
  
## <a name="options"></a>選項。  
 **[預設管道]**  
 指定「具名管道網路」程式庫嘗試連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的目標執行個體時要使用的預設管道。 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會接聽： `\\.\pipe\sql\query`  
  
 若要連接到預設管道，請輸入 `sql\query`  
  
 **已啟用**  
 可能的值為 [是] 和 [否]。  
  
## <a name="see-also"></a>另請參閱  
 [選擇網路通訊協定](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
