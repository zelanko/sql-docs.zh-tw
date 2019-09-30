---
title: 管理 CDC 服務 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- manSer
ms.assetid: 645ae53f-f352-4d6a-9eb0-264e53a93a18
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b6838ae985c16f4188ed43e3442b4f86c4a3557b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298681"
---
# <a name="manage-a-cdc-service"></a>管理 CDC 服務

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  您可以使用 CDC 設計工具主控台來檢視以 CDC 服務組態主控台建立的服務，並在 Oracle CDC 服務中管理所有執行個體。  
  
 在左窗格中按一下服務名稱，以顯示有關此服務的資訊並加以管理。  
  
> [!NOTE]  
>  您必須先使用 CDC 服務組態主控台在此清單中加入服務，以建立服務。 如需有關如何建立服務的詳細資訊，請參閱 CDC 服務組態主控台提供的線上說明。  
  
## <a name="what-you-can-do-when-you-display-the-cdc-service-information"></a>您在顯示 CDC 服務資訊時可以做什麼事  
 當您顯示有關服務的資訊時，可以執行以下作業：  
  
 **針對選取的服務建立新的 CDC 執行個體**  
  
 在右窗格中按一下 **[新增 Oracle CDC 執行個體]** ，建立該服務的新執行個體。 隨即開啟新增執行個體精靈來建立執行個體。 如需有關新增執行個體精靈的詳細資訊，請參閱＜ [Use the New Instance Wizard](../../integration-services/change-data-capture/use-the-new-instance-wizard.md)＞。  
  
 **在服務中啟動所有 CDC 執行個體**  
  
 在右窗格中按一下 **[啟動所有執行個體]** ，開始從服務中定義的所有執行個體擷取資料。  
  
 **在服務中停止所有 CDC 執行個體**  
  
 按一下 **[停止所有執行個體]** ，針對服務中的所有執行個體停止異動資料擷取。  
  
## <a name="see-also"></a>另請參閱  
 [如何建立 SQL Server 變更資料庫執行個體](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [如何從 CDC 設計工具主控台管理 CDC 服務](../../integration-services/change-data-capture/how-to-manage-a-cdc-service-from-the-cdc-designer-console.md)   
 [Use the New Instance Wizard](../../integration-services/change-data-capture/use-the-new-instance-wizard.md)  
  
  
