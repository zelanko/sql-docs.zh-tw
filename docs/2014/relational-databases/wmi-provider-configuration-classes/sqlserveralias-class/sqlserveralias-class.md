---
title: SqlServerAlias 類別 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SqlServerAlias Class
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SqlServerAlias class
ms.assetid: 475662b9-6985-45bf-b1e9-b0f26ef50443
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 01e66c9362a8e1c91bd43e4d6821e12f93d23152
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033891"
---
# <a name="sqlserveralias-class"></a>SqlServerAlias 類別
  [SqlServerAlias 類別](sqlserveralias-class.md)類別代表伺服器連接別名。  
  
 當以下兩個情況同時發生時，就需要伺服器連接別名。  
  
-   用戶端連接到的執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]透過不是預設網路傳輸的網路傳輸。  
  
-   用戶端連接的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體會接聽替代具名管道。  
  
 **注意：** [SqlServerAlias 類別](sqlserveralias-class.md)繼承`Put`來自提供者類別的方法。 但是，它不會傳回如 `Provider::Put` 方法指示的任何結果。 如需詳細資訊，請參閱 WMI 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [設定用戶端通訊協定](http://technet.microsoft.com/library/ms181035.aspx)  
  
  