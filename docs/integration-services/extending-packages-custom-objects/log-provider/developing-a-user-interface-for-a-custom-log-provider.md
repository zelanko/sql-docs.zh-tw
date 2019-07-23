---
title: 開發自訂記錄提供者的使用者介面 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services], custom log providers
- custom log providers [Integration Services], developing custom user interface
ms.assetid: 6fd2d269-d87a-4134-82a1-40a09b3b5453
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f3dccd3641592ebaadb7df3dd467cb28cf9a617f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062940"
---
# <a name="developing-a-user-interface-for-a-custom-log-provider"></a>開發自訂記錄提供者的使用者介面

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  許多 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 記錄提供者都有自訂使用者介面，以實作 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI>，以及使用可用連線管理員的篩選下拉式清單，取代 [設定 SSIS 記錄]  對話方塊中的 [設定]  文字方塊。 不過，在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中並未實作自訂記錄提供者的自訂使用者介面。  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂記錄提供者](../../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)   
 [撰寫自訂記錄提供者程式碼](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)  
  
  
