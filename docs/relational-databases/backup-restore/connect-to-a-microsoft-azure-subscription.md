---
title: 連接至 Microsoft Azure 訂用帳戶 | Microsoft Docs
description: 向 SQL Server 執行個體註冊 Azure Blob 容器，以建立共用存取簽章、預存的存取原則，以及 SQL Server 認證。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: cca5a270-643f-4677-8802-98464f19f82a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 974086bc61e2f40819c77693a6033aac512893ac
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829754"
---
# <a name="connect-to-a-microsoft-azure-subscription"></a>連接至 Microsoft Azure 訂用帳戶
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
使用 [連接至 Microsoft 訂用帳戶]  向 SQL Server 執行個體註冊現有的 Azure blob 容器。  對話方塊會在 Azure blob 容器上建立共用的存取簽章和預存的存取原則，再建立 SQL Server 認證。  從 SQL Server Management Studio 使用 [備份或還原] 工作，且作業牽涉到 URL 裝置時，就會出現此對話方塊。

## <a name="limitation"></a>限制
[連接至 Microsoft 訂用帳戶]  只適用於透過服務管理 (傳統) 部署模型建立的 Azure 儲存體帳戶。  如需有關 Azure 部署模型的詳細資訊，請參閱 [Azure Resource Manager vs. 傳統部署：了解資源的部署模型和狀態](https://azure.microsoft.com/documentation/articles/resource-manager-deployment-model/)。

## <a name="options"></a>選項。
**登入**     
使用適當的 Azure 帳戶登入。

**選取要使用的訂閱**      
從下拉式清單中選取所需的訂閱。

**選取儲存體帳戶**  
從下拉式清單中選取所需的儲存體帳戶。

**選取 Blob 容器**   
從下拉式清單中選取所需的 Blob 容器。

**共用存取原則到期**   
共用的存取原則會在指定的日期到期。  預設到期日是自建立時起算一年。  視需要修改。

**已產生共用存取簽章**   
RTF 方塊會顯示已產生的共用存取簽章。

**建立認證**   
按鈕會產生預存的存取原則和共用的存取簽章，然後建立 SQL Server 認證。
