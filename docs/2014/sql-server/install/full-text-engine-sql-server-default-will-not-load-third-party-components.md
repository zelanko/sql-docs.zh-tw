---
title: Microsoft Full-text Engine for SQL Server 不會載入預設的不帶正負號的第三方元件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Full-Text Engine for SQL service
- MSFTESQL service
ms.assetid: 029f9895-7232-4149-9362-3ab1a4133d21
caps.latest.revision: 20
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b6c3adecfac495a72a86b093113c67d19bb9e7e0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37244218"
---
# <a name="the-microsoft-full-text-engine-for-sql-server-will-not-load-unsigned-third-party-components-by-default"></a>Microsoft Full-Text Engine for SQL Server 預設不會載入未簽署的協力廠商元件
  根據預設，[!INCLUDE[msCoName](../../includes/msconame-md.md)] Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會載入未經 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 簽署的元件。  
  
## <a name="component"></a>元件  
 全文檢索搜尋  
  
## <a name="description"></a>描述  
 升級之後，[!INCLUDE[msCoName](../../includes/msconame-md.md)] Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設不會載入目前安裝在伺服器上的協力廠商篩選，例如 PDF 篩選。  
  
## <a name="corrective-action"></a>更正動作  
 若要載入的協力廠商篩選，您必須設定*load_os_resource*並關閉*verify_signature*該執行個體上。  
  
## <a name="see-also"></a>另請參閱  
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
