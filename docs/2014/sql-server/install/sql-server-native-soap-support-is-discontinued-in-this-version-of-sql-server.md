---
title: 這個版本的 SQL Server 已停止支援 SQL Server 原生 SOAP。 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 80fd692b-1cea-4139-8e80-454d3e81c76d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9c3af432ac614a11bb6321af87e28f9675f806a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183808"
---
# <a name="sql-server-native-soap-support-is-discontinued-in-this-version-of-sql-server"></a>這個版本的 SQL Server 已停止支援 SQL Server 原生 SOAP。
  Upgrade Advisor 偵測到您使用了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生 XML Web Service。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中已移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生 XML Web Service。  
  
## <a name="discovering-where-you-use-native-xml-web-services"></a>探索使用原生 XML Web Service 的地方  
 您可以看到應用程式使用原生 XML Web Service 的地方，如下所示：  
  
-   當您執行 Upgrade Advisor 時。  
  
-   當您升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本時。  
  
## <a name="corrective-action"></a>更正動作  
 修改目前使用原生 XML Web Service 的應用程式。  
  
  
