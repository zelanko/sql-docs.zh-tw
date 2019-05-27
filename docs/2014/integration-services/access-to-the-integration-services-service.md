---
title: 存取 Integration Services 服務 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- viewing packages while running
- displaying packacges while running
- security [Integration Services], running packages
- packages [Integration Services], security
- current packages running
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 1088aafc-14c5-4e7d-9930-606a24c3049b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e3654be0afe51be6566a09897a2656dd53c77696
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062240"
---
# <a name="access-to-the-integration-services-service"></a>對 Integration Services 服務的存取權
  封裝保護等級可限制已獲允許編輯和執行封裝的人員。 您需要額外的保護措施來限制有誰能夠檢視目前在伺服器上執行的封裝清單，以及有誰能夠停止目前在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中執行的封裝。  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 會使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務列出正在執行封裝。 Windows Administrators 群組的成員可以檢視和停止所有目前正在執行封裝。 非 Administrators 群組成員的使用者只能檢視和停止他們所啟動的封裝。  
  
 限制存取執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務的電腦很重要，特別是可列舉遠端資料夾的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務。 任何已驗證的使用者都可以要求列舉封裝。 服務即使找不到該服務，仍會列舉資料夾。 這些資料夾名稱對惡意使用者可能很有用。 如果管理員已設定服務來列舉遠端電腦上的資料夾，則使用者還可查看他們通常無法看到的資料夾名稱。  
  
  
