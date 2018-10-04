---
title: LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
ms.assetid: a7c5ce08-8841-49a3-b252-116807ba469a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d56dbcb5fe1d37e3fce223bc910830b063484aa5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117448"
---
# <a name="localdberrorinstanceexistswithlowerversion"></a>LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|258|  
|事件來源|SQL Server 本機資料庫執行階段 12.0|  
|元件|本機資料庫執行階段 API|  
|訊息文字|無法以指定的版本建立本機資料庫執行個體。 已存在相同名稱之執行個體，但其版本較指定的版本舊。|  
  
## <a name="explanation"></a>說明  
 指定的執行個體已經存在，但是其版本低於要求的版本。  
  
## <a name="user-action"></a>使用者動作  
 請刪除現有的執行個體，然後再重試作業。  
  
  
