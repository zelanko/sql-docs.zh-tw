---
title: SqlServerAlias 類別
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- SqlServerAlias Class
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServerAlias class
ms.assetid: 475662b9-6985-45bf-b1e9-b0f26ef50443
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 18d6cfd0b2d0184e5bf667fc12f57a6c0dcf5025
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753728"
---
# <a name="sqlserveralias-class"></a>SqlServerAlias 類別
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  [SqlServerAlias 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)代表伺服器連接別名。  
  
 當以下兩個情況同時發生時，就需要伺服器連接別名。  
  
-   用戶端透過 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不是預設網路傳輸的網路傳輸來連接的實例。  
  
-   用戶端連接的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體會接聽替代具名管道。  
  
 **注意：**[SqlServerAlias 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)會從 Provider 類別繼承**Put**方法。 不過，它不會傳回**提供者：:P**的工作方法所指出的任何結果。 如需詳細資訊，請參閱 WMI 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
