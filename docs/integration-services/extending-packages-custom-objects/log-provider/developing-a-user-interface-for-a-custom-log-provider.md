---
title: 開發自訂記錄提供者的使用者介面 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom user interface [Integration Services], custom log providers
- custom log providers [Integration Services], developing custom user interface
ms.assetid: 6fd2d269-d87a-4134-82a1-40a09b3b5453
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7d4173c215200f0b5cb17f68001dfcf21d4f42d9
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35331312"
---
# <a name="developing-a-user-interface-for-a-custom-log-provider"></a>開發自訂記錄提供者的使用者介面
  許多 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 記錄提供者都有自訂使用者介面，以實作 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI>，以及使用可用連線管理員的篩選下拉式清單，取代 [設定 SSIS 記錄] 對話方塊中的 [設定] 文字方塊。 不過，在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中並未實作自訂記錄提供者的自訂使用者介面。  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂記錄提供者](../../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)   
 [撰寫自訂記錄提供者程式碼](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)  
  
  
