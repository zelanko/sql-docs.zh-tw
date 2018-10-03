---
title: Integration Services 參數 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, parameters
ms.assetid: b1bb3ea3-8097-4e76-b9c2-78a0f46a23bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2b2b9fc62d26edbac0244bed07d20931fbb508f8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210378"
---
# <a name="integration-services-parameters"></a>Integration Services 參數
  針對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，您可以決定要分析[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]封裝的電腦上，或[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]檔案封裝在檔案系統中。 如果您要分析檔案系統中的檔案，請提供包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝之資料夾的路徑。  
  
## <a name="options"></a>選項。  
 **分析電腦上的 SSIS 封裝**  
 選取此選項，即可分析電腦上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。 依預設，會選取這個選項。  
  
 **分析 SSIS 封裝檔案**  
 選取此選項，即可分析檔案系統中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
 **SSIS 封裝的路徑**  
 找出保存 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的 UNC 或本機路徑。 您不需要加入檔案名稱。 如果無法存取您所輸入的路徑，就無法按**下一步**。 根據預設，此路徑是空白的。 只有當您選取時，這個欄位啟用**分析 SSIS 封裝檔案**。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Upgrade Advisor](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Upgrade Advisor 使用者介面參考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
