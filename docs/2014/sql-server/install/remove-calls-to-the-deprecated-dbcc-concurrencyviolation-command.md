---
title: 移除對已被取代之 DBCC CONCURRENCYVIOLATION 命令的呼叫 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0110d4bc138ad0da953eb83d3c81ec265d2fd3ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093210"
---
# <a name="remove-calls-to-the-deprecated-dbcc-concurrencyviolation-command"></a>移除已被取代之 DBCC CONCURRENCYVIOLATION 命令的呼叫
  Upgrade Advisor 偵測到您使用了 DBCC CONCURRENCYVIOLATION 命令。 無法再使用這個命令。 執行這個命令會傳回錯誤 2526。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 由於沒有任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的最新版本包含工作負載管理員，因此這個命令已經移除了。  
  
## <a name="corrective-action"></a>更正動作  
 請更新應用程式和指令碼，以便移除這個已被取代之命令的參考。  
  
## <a name="external-resources"></a>外部資源  
  
