---
title: 應用程式定義域和 CLR 整合安全性 |Microsoft 文件
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
helpviewer_keywords:
- security [CLR integration]
- application domains [CLR integration]
ms.assetid: 54ee904e-e21a-4ee7-b4ad-a6f6f71bd473
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0c97f958126dc7b19478bf0864a23ce4ab4fe07b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033326"
---
# <a name="application-domains-and-clr-integration-security"></a>應用程式網域和 CLR 整合安全性
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會載入屬於同一應用程式網域中相同擁有者的組件。 組件可透過在同一應用程式網域中執行的一組組件，使用 .NET Framework Reflection 應用程式開發介面或其他方式在執行時互相發現對方，並能夠以晚期繫結方式呼叫彼此內部。 因為此類呼叫是針對屬於同一擁有者的組件而進行，所以不會檢查這些呼叫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 權限。 應用程式網域中組件的位置配置設計主要是為達成延展性、安全性及隔離目的，並可能在以後的版本中變更。 因此，您不應依賴透過晚期繫結機制，在同一應用程式網域中尋找組件。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  