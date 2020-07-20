---
title: 檢視資源健全狀況原則結果 (SQL Server 公用程式) | Microsoft 文件
description: 了解如何使用 SQL Server Management Studio 來檢視 SQL Server 執行個體及資料層應用程式的 SQL Server 公用程式資源健康情況原則結果。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 83cbdce1203cbe28f58c676da361091880a9f675
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197247"
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>檢視資源健全狀況原則結果 (SQL Server 公用程式)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用公用程式儀表板，針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體和資料層應用程式檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式資源參數。 如需詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  

##  <a name="SSMSProcedure"></a>

### <a name="view-sql-server-utility-resource-health-policy-results"></a>檢視 SQL Server 公用程式資源健全狀況原則結果  

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中，依序選取 [檢視] 和 [公用程式總管]，以檢視 [公用程式總管] 瀏覽窗格。 若要檢視此內容窗格，請依序選取 [檢視] 和 [公用程式總管內容]。  

2. 在瀏覽窗格中，選取 ![連接到公用程式](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")[連接到公用程式]。 如果您尚未建立公用程式控制點 (UCP) 或是您尚未將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體或資料層應用程式註冊到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內，請參閱 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  

3. 選取 [UCP] 節點，以檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受控執行個體和資料層應用程式的摘要資料 (按一下滑鼠右鍵重新整理)。 儀表板資料會顯示在內容窗格中。  

4. 選取 [受控執行個體] 節點，以檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受控執行個體的清單檢視資料 (按一下滑鼠右鍵重新整理)。 清單檢視資料會顯示在內容窗格中。  

5. 選取 [部署的資料層應用程式] 節點，以檢視資料層應用程式的清單檢視資料 (按一下滑鼠右鍵重新整理)。 清單檢視資料會顯示在內容窗格中。  

## <a name="see-also"></a>另請參閱

- [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)
- [降低 CPU 使用量原則的雜訊 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)
- [部署的資料層應用程式詳細資料 &#40;SQL Server 公用程式&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867) (機器翻譯)
- [受控執行個體詳細資料 &#40;SQL Server 公用程式&#41;](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2) (機器翻譯)
- [公用程式管理 &#40;SQL Server 公用程式&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)