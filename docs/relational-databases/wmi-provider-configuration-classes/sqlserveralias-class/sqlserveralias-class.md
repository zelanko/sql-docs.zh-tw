---
title: SqlServerAlias 類別 |Microsoft Docs
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
ms.openlocfilehash: cdcbd34978738d64d52b3c70a280507b6cb0c391
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68052372"
---
# <a name="sqlserveralias-class"></a>SqlServerAlias 類別
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [SqlServerAlias 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)類別代表伺服器連接別名。  
  
 當以下兩個情況同時發生時，就需要伺服器連接別名。  
  
-   用戶端連接到執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]透過不是預設網路傳輸的網路傳輸。  
  
-   用戶端連接的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體會接聽替代具名管道。  
  
 **注意：** [SqlServerAlias 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)繼承**放**從 Provider 類別的方法。 不過，它不會傳回任何結果所示**Provider::Put**方法。 如需詳細資訊，請參閱 WMI 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
