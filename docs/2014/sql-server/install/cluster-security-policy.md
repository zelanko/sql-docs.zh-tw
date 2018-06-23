---
title: 叢集安全性原則 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- cluster security policy
ms.assetid: 38afa421-2599-404f-8ba6-172668c6325e
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c545910e455d77cf17e944138a6edc902565c656
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133864"
---
# <a name="cluster-security-policy"></a>叢集安全性原則
  使用 [叢集安全性原則] 頁面，即可針對容錯移轉叢集執行個體設定安全性原則。  
  
## <a name="options"></a>選項。  
 針對叢集服務指定全域或本機網域群組。 所有資源權限都是由包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶當做群組成員的網域層級群組所控制。 如需 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]之服務安全性識別碼 (SID) 功能的詳細資訊，請參閱 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
  