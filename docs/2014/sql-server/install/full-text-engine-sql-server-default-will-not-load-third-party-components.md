---
title: 適用于 SQL Server 的 Microsoft 全文檢索引擎不會預設載入未簽署的協力廠商元件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Full-Text Engine for SQL service
- MSFTESQL service
ms.assetid: 029f9895-7232-4149-9362-3ab1a4133d21
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 12ff188fb6aa6ac286817a7cc1c3ad726483c886
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012483"
---
# <a name="the-microsoft-full-text-engine-for-sql-server-will-not-load-unsigned-third-party-components-by-default"></a>Microsoft Full-Text Engine for SQL Server 預設不會載入未簽署的協力廠商元件
  根據預設，[!INCLUDE[msCoName](../../includes/msconame-md.md)] Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會載入未經 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 簽署的元件。  
  
## <a name="component"></a>元件  
 全文檢索搜尋  
  
## <a name="description"></a>描述  
 升級之後，[!INCLUDE[msCoName](../../includes/msconame-md.md)] Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設不會載入目前安裝在伺服器上的協力廠商篩選，例如 PDF 篩選。  
  
## <a name="corrective-action"></a>更正動作  
 若要載入協力廠商篩選，您必須設定*load_os_resource* ，並關閉該實例上的*verify_signature* 。  
  
## <a name="see-also"></a>另請參閱  
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
